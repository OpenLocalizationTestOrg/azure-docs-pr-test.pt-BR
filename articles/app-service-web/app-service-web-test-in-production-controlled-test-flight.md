---
title: "implantação de aaaFlighting (teste beta) no serviço de aplicativo do Azure"
description: "Saiba como tooflight novos recursos no seu aplicativo ou beta testar as atualizações neste tutorial de ponta a ponta. Ele reúne os recursos do Serviço de Aplicativo como publicação contínua, slots, roteamento de tráfego e integração do Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Implantação flighting (teste beta) no Serviço de Aplicativo do Azure
Este tutorial mostra como toodo *implantações flighting* integrando Olá diversos recursos de [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e [Azure Application Insights](/services/application-insights/).

*Flighting* é um processo de implantação que valida um novo recurso ou alteração com um número limitado de clientes reais, e é um teste importante no cenário de produção. É toobeta parecido testes e às vezes é conhecido como "teste controlado voo". Muitas grandes empresas com uma presença na Web usam essa abordagem para obter validação antecipada sobre suas atualizações de aplicativo em sua prática de [desenvolvimento ágil](https://en.wikipedia.org/wiki/Agile_software_development). Serviço de aplicativo do Azure permite que você teste toointegrate em produção com a publicação contínua e Application Insights tooimplement Olá mesmo cenário DevOps. Entre os benefícios dessa abordagem estão:

* **Obter comentários real *antes de* atualizações são lançada tooproduction** -Olá somente coisa melhor do que obter comentários assim que você soltar é obter comentários antes de liberar. Você pode testar atualizações com o tráfego de usuário real e comportamentos antecipada desejados no ciclo de vida do hello.
* **Aprimore o [CTDD (desenvolvimento contínuo controlado por testes)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - ao integrar o teste em produção com a integração e instrumentação contínuas com o Application Insights, a validação do usuário ocorre automaticamente e desde o início do ciclo de vida do produto. Isso ajuda a reduzir os investimentos em tempo na execução de teste manual.
* **Otimizar o fluxo de trabalho de teste** -através da automação de teste em produção com a instrumentação de monitoramento contínua, você pode potencialmente atingir Olá objetivos de vários tipos de testes em um único processo, como [integração](https://en.wikipedia.org/wiki/Integration_testing), [regressão](https://en.wikipedia.org/wiki/Regression_testing), [usabilidade](https://en.wikipedia.org/wiki/Usability_testing), acessibilidade, localização, [desempenho](https://en.wikipedia.org/wiki/Software_performance_testing), [segurança](https://en.wikipedia.org/wiki/Security_testing), e [ aceitação](https://en.wikipedia.org/wiki/Acceptance_testing).

Uma implantação flighting não se trata apenas do roteamento de tráfego em tempo real. Em tal implantação deseja toogain insight assim que possível, se é um erro inesperado, degradação de desempenho, problemas de experiência do usuário. Lembre-se de que você está lidando com clientes reais. Caso toodo à direita, você deve garantir que você configurou seu toogather implantação flighting todos os dados de saudação, você precisa em ordem toomake uma decisão informada para a próxima etapa. Este tutorial mostra como toocollect dados com o Application Insights, mas você podem usar o New Relic ou outras tecnologias que atenda às seu cenário.

## <a name="what-you-will-do"></a>O que você fará
Neste tutorial, você aprenderá como toobring Olá tootest juntos cenários a seguir em seu aplicativo de serviço de aplicativo em produção:

* [Rotear o tráfego de produção](app-service-web-test-in-production-get-start.md) tooyour beta aplicativo
* [Instrumentar seu aplicativo](../application-insights/app-insights-web-track-usage.md) métricas úteis tooobtain
* Implantar continuamente seu aplicativo beta e rastrear métricas de aplicativo em tempo real
* Métricas de comparação entre o aplicativo de produção de hello e Olá beta aplicativo toosee como código altera traduzem tooresults

## <a name="what-you-will-need"></a>O que será necessário
* Uma conta do Azure
* Uma conta do [GitHub](https://github.com/)
* Visual Studio 2015 - você pode baixar Olá [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Shell de Git (instalado com [GitHub para Windows](https://windows.github.com/))-isso permite que você toorun os dois comandos Git e do PowerShell de Olá no hello mesma sessão
* Bits do [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) mais recentes
* Noções básicas sobre a seguir hello:
  * Implantação do modelo do [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (veja [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Você precisa de uma conta do Azure toocomplete neste tutorial:
>
> * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados você pode manter a conta de saudação e use livre serviços do Azure, como aplicativos Web.
> * É possível [ativar os benefícios para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) – todos os meses, sua assinatura do Visual Studio concede créditos que podem ser usados para experimentar serviços pagos do Azure.
>
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
>
>

## <a name="set-up-your-production-web-app"></a>Configurar seu aplicativo Web de produção
> [!NOTE]
> script Hello usado neste tutorial automaticamente irá configurar a publicação contínua de seu repositório GitHub. Isso exige que suas credenciais do GitHub já são armazenados no Azure, caso contrário, a implantação de Olá script falhará durante a tentativa de tooconfigure configurações de controle de origem para os aplicativos web hello.
>
> toostore seu GitHub credenciais no Azure, criar um aplicativo web no hello [Portal do Azure](https://portal.azure.com/) e [configurar implantação GitHub](app-service-continuous-deployment.md). Você só precisa toodo desta vez.
>
>

Em um cenário típico de DevOps, você tem um aplicativo que está em execução no Azure e desejar toomake tooit de alterações por meio da publicação contínua. Nesse cenário, você implantará tooproduction um modelo que você foram desenvolvidos e testados.

1. Criar seu próprio bifurcação de saudação [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositório. Para obter informações sobre como criar a bifurcação, consulte [Bifurcar um repositório](https://help.github.com/articles/fork-a-repo/). Depois que a bifurcação é criada, você pode vê-la no navegador.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Abra uma sessão do Git Shell. Se ainda não tiver o Git Shell, instale o [GitHub para Windows](https://windows.github.com/) agora.
3. Crie um clone local de sua bifurcação executando Olá comando a seguir:

     git clone https://github.com/<your_fork>/ToDoApp.git
4. Uma vez que o clone local, navegue muito*&lt;repository_root >*\ARMTemplates e execução Olá deploy.ps1 script com um sufixo exclusivo, conforme mostrado abaixo:

     .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix>
5. Quando solicitado, digite Olá desejado de nome de usuário e senha para acesso ao banco de dados. Lembre-se de credenciais de seu banco de dados, pois você precisará toospecify-las novamente quando atualizar Olá grupo de recursos.

   Você deve ver Olá provisionamento progresso de vários recursos do Azure. Quando a implantação for concluída, o script hello Iniciar aplicativo hello no navegador hello e oferecem um bipe amigável.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. De volta à sessão do Git Shell, execute:

     .\swap –Name ToDoApp<your_suffix>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Quando o script hello termina, volte toobrowse toohello endereço do front-end (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) aplicativo hello de toosee em execução em produção.
8. Faça logon no hello [Portal do Azure](https://portal.azure.com/) e veja o que é criado.

   Você deve ser capaz de toosee dois os aplicativos web no hello mesmo grupo de recursos, um com hello `Api` sufixo no nome de saudação. Se você examinar o modo de exibição de grupo de recursos Olá, você também verá Olá banco de dados SQL e servidor, Olá plano de serviço de aplicativo e slots de preparo Olá para aplicativos da web de saudação. Navegue pelos recursos diferentes hello e compará-los com  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json como eles são configurados no modelo de saudação.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Você configurou o aplicativo de produção de hello.  Agora, vamos imaginar que você receba comentários que usabilidade é ruim para o aplicativo hello. Portanto, você decide tooinvestigate. Você vai tooinstrument toogive seu aplicativo você comentários.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Investigue: instrumentar o aplicativo cliente para monitoramento/métricas
1. Abra *&lt;raiz_do-repositório>*\src\MultiChannelToDo.sln in Visual Studio.
2. Restaure todos os pacotes NuGet clicando com o botão direito do mouse na solução > **Gerenciar Pacotes NuGet da Solução** > **Restaurar**.
3. Clique com botão direito **MultiChannelToDo.Web** > **adicionar telemetria do Application Insights** > **configurar** > alterar o grupo de recursos tooToDoApp*&lt;your_suffix >* > **tooProject adicionar Application Insights**.
4. Em Olá Portal do Azure, abra a folha de saudação para Olá **MultiChannelToDo.Web** recurso do Application Insight. Em seguida, em hello **integridade do aplicativo** parte, clique em **Saiba como a página do navegador toocollect carregar dados** > Copiar código.
5. Adicionar Olá copiado o código de instrumentação JS muito*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml logo antes de fechamento Olá `<heading>` marca. Ela deve conter a chave de instrumentação exclusivo de saudação do recurso Application Insight.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Envie eventos personalizados tooApplication Insights para cliques adicionando Olá inferior do código toohello do corpo a seguir:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Este trecho de código JavaScript envia um evento personalizado tooApplication Insights toda vez que um usuário clica em qualquer lugar no aplicativo web de saudação.
7. No Shell de Git, confirmar e enviar por push a bifurcação de tooyour alterações no GitHub. Em seguida, aguarde o navegador de toorefresh de clientes.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Saudação de permuta implantado tooproduction de alterações do aplicativo:

     .\swap –Name ToDoApp<your_suffix>
9. Procure o recurso do Application Insights toohello que você configurou. Clique em Eventos personalizados.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Se você não vir as métricas para eventos personalizados, aguarde alguns minutos e clique em **Atualizar**.

Suponha que você veja um gráfico como o mostrado abaixo:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

E a grade de eventos Olá abaixo dele:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

De acordo com o código do aplicativo ToDoApp tooyour, Olá **botão** evento corresponde toohello no botão Enviar e hello **entrada** evento corresponde a caixa de texto toohello. Até agora, as coisas fazem sentido. No entanto, parece que há uma boa quantidade de cliques e cliques muito poucos itens de tarefas pendentes de hello (Olá **LI** eventos).

Com base nesse, você formulário sua hipótese que alguns usuários confundido qual parte da saudação interface do usuário é clicável e isso ocorre porque o estilo do cursor Olá para seleção de texto quando ele for colocado em itens de lista hello e seus ícones.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Isso pode ser um exemplo forçado. No entanto, você está indo toomake um aplicativo de tooyour aperfeiçoamento e, em seguida, executar um flighting comentários de usabilidade de tooget de implantação de clientes em tempo real.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumentar seu aplicativo de servidor para monitoramento/métricas
Isso é uma tangente pois cenário Olá demonstrado neste tutorial lida apenas transações com hello aplicativo de cliente. No entanto, para fins de integridade você configurará saudação do servidor app.

1. Clique com botão direito **MultiChannelToDo** > **adicionar telemetria do Application Insights** > **configurar** > alterar o grupo de recursos tooToDoApp*&lt;your_suffix >* > **tooProject adicionar Application Insights**.
2. No Shell de Git, confirmar e enviar por push a bifurcação de tooyour alterações no GitHub. Em seguida, aguarde o navegador de toorefresh de clientes.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Saudação de permuta implantado tooproduction de alterações do aplicativo:

     .\swap –Name ToDoApp<your_suffix>

É isso!

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Investigue: Adicionar métricas de aplicativo de cliente de tooyour marcas específicas de slot
Nesta seção, você irá configurar Olá diferentes de implantação slots toosend telemetria específicos de slot toohello mesmo recurso Application Insights. Dessa forma, você pode comparar a telemetria de dados entre o tráfego de slots diferentes (ambientes de implantação) tooeasily ver o efeito de saudação de suas alterações de aplicativo. AT Olá mesmo tempo, você pode separar o tráfego de produção de hello restante Olá para que você possa continuar toomonitor seu aplicativo de produção conforme necessário.

Desde que você está coletando dados sobre o comportamento do cliente, você vai [adicionar um inicializador de telemetria tooyour código JavaScript](../application-insights/app-insights-api-filtering-sampling.md) em cshtml. Se você quiser tootest desempenho do lado do servidor, por exemplo, você também pode fazer da mesma forma no código do servidor (consulte [API do Application Insights para métricas e eventos personalizados](../application-insights/app-insights-api-custom-events-metrics.md).

1. Primeiro, adicione Olá bewteen de código Olá dois `//` comentários abaixo no bloco de JavaScript Olá que você adicionou toohello `<heading>` marca anteriormente.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Esse código de inicializador causa Olá `appInsights` tooadd objeto Olá uma propriedade personalizada chamada `Environment` tooevery parte de telemetria que ele envia.
2. Em seguida, adicione essa propriedade personalizada como uma [configuração do slot](web-sites-staged-publishing.md#AboutConfiguration) de seu aplicativo Web no Azure. toodo, Olá executar comandos a seguir em sua sessão do Shell do Git.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Olá Web. config em seu projeto já define Olá `environment` configuração do aplicativo. Com essa configuração, quando você testar o aplicativo de saudação localmente, suas métricas serão marcadas com `VS Debugger`. No entanto, quando você enviar por push tooAzure suas alterações, Azure encontrará e usar Olá `environment` configuração em vez disso, na configuração do aplicativo da web de saudação do aplicativo e suas métricas serão marcados com `Production`.
3. Confirmar e enviar por push a bifurcação de tooyour de alterações de código no GitHub e aguarde até que os usuários toouse Olá novo aplicativo (necessidade toorefresh Olá navegador). Ocupa cerca de 15 minutos para Olá nova propriedade tooshow em suas ideias de aplicativo `MultiChannelToDo.Web` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Agora, vamos toohello **eventos personalizados** folha novamente e filtro Olá métricas em `Environment=Production`. Agora você deve ser capaz de toosee todos os Olá novos eventos personalizados em produção de hello slot com esse filtro.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Clique em Olá **Favoritos** como botão toosave Olá atual do Metrics Explorer configurações toosomething **eventos personalizados: produção**. Você pode alternar facilmente entre esta exibição e uma exibição de slot de implantação posteriormente.

   > [!TIP]
   > Para uma análise ainda mais eficiente, considere [integrar seu recurso do Application Insights com o Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Adicionar marcas específicas do slot tooyour aplicativo métricas
Novamente, para fins de integridade você configurará saudação do servidor app. Ao contrário do aplicativo de cliente de saudação que é instrumentado em JavaScript, marcas específicas do slot de saudação do aplicativo de servidor é instrumentada com o código .NET.

1. Abra *&lt;raiz_do_repositório>*\src\MultiChannelToDo\Global.asax.cs. Adicione bloco de código Olá abaixo, antes de saudação chave de fechamento namespace.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Corrija os erros de resolução de nome hello adicionando Olá `using` instruções abaixo toohello a partir do arquivo hello:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Adicione código Olá abaixo toohello início Olá `Application_Start()` método:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Confirmar e enviar por push a bifurcação de tooyour de alterações de código no GitHub e aguarde até que os usuários toouse Olá novo aplicativo (necessidade toorefresh Olá navegador). Ocupa cerca de 15 minutos para Olá nova propriedade tooshow em suas ideias de aplicativo `MultiChannelToDo` recursos.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Atualização: configurar sua ramificação beta
1. Abra  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json e localizar Olá `appsettings` recursos (procure `"name": "appsettings"`). Há quatro deles, um para cada slot.
2. Para cada `appsettings` recurso, adicione uma `"environment": "[parameters('slotName')]"` final de toohello de configuração de aplicativo da saudação `properties` matriz. Não se esqueça de linha anterior do hello tooend com uma vírgula.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Você acabou de adicionar Olá `environment` definindo tooall slots Olá no modelo de saudação do aplicativo.
3. No hello mesmo arquivo, localize Olá `slotconfignames` recursos (procure `"name": "slotconfignames"`). Há dois deles, um para cada aplicativo.
4. Para cada `slotconfignames` recurso, adicione `"environment"` toohello final de saudação `appSettingNames` matriz. Não se esqueça de linha anterior do hello tooend com uma vírgula.

    Você acabou de criar hello `environment` slot de implantação do respectivos de tooits do aplicativo configuração cartão para ambos os aplicativos.  
5. Na sua sessão do Shell de Git, Olá execução seguintes comandos com hello mesmo sufixo de grupo de recursos que você usou.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Quando solicitado, especifique Olá as mesmas credenciais de banco de dados SQL como antes. Em seguida, quando solicitado a grupo de recursos tooupdate hello, tipo `Y`, em seguida, `ENTER`.

    Depois que o script hello termina, todos os seus recursos no grupo de recursos original Olá são mantidos, mas um novo slot denominado "beta" for criado com hello mesmo configuração como o slot de "Preparação" hello que foi criado no início de saudação.

   > [!NOTE]
   > Esse método de criação de ambientes de implantação diferentes é diferente do método hello em [desenvolvimento de software Agile com serviço de aplicativo do Azure](app-service-agile-software-development.md). Aqui, você cria ambientes de implantação com slots de implantação, enquanto que lá você cria ambientes de implantação com grupos de recursos. Gerenciando ambientes de implantação com grupos de recursos permite que você toodevelopers fora dos limites do ambiente tookeep Olá produção, mas não é fácil toodo teste em produção, o que pode ser feito facilmente com slots.
   >
   >

Se desejar, você também pode criar um aplicativo alfa executando

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Para este tutorial, você continuará usando seu aplicativo beta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Atualização: Seu aplicativo de beta de toohello de atualizações por Push
Faça tooyour aplicativo que você deseja tooimprove.

1. Verifique se você está agora em sua ramificação beta

        git checkout beta
2. Em  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, localizar Olá `<li>` marcar e adicionar Olá `style="cursor:pointer"` atributo, conforme mostrado abaixo.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. Confirmar e enviar por push tooAzure.
4. Verifique se a alteração Olá agora é refletida no slot de beta Olá navegando toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Se você não vir Olá alterar ainda, atualize seu código javascript novo navegador tooget hello.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Agora que você tem a alteração em execução no slot de beta hello, você está pronto tooperform uma implantação flighting.

## <a name="validate-route-traffic-toohello-beta-app"></a>Validar: Aplicativo de beta toohello de tráfego de rota
Nesta seção, você será rotear tráfego toohello beta aplicativo. Para fins de clareza da demonstração, você vai tooroute uma parte significativa da saudação tooit de tráfego de usuário. Na realidade, Olá quantidade de tráfego que você deseja tooroute dependerá de sua situação específica. Por exemplo, se seu site estiver em escala de saudação do microsoft.com, talvez seja necessário menor que um por cento de seu tráfego total de dados de pedidos toogain útil.

1. Na sua sessão do Shell de Git, execute Olá tooroute comandos a seguir metade do slot de beta Olá produção tráfego toohello:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Olá `ReroutePercentage=50` propriedade especifica que 50% do tráfego de produção de hello será a URL do aplicativo do toohello roteados beta (especificado pelo Olá `ActionHostName` propriedade).
2. Agora vá toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% de tráfego Olá agora deve ser redirecionado toohello slot de beta.
3. Em seu recurso Application Insights, filtrar métricas Olá pelo ambiente = "beta".

   > [!NOTE]
   > Se você salvar essa exibição filtrada como favorito outro, pode inverter facilmente exibições de métrica explorer Olá entre modos de exibição do beta e de produção.
   >
   >

Suponha que no Application Insights, consulte a seguir toohello algo semelhante:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Não só é isso mostra que há muitos cliques mais em Olá `<li>` marcas, mas parece toobe um surto de cliques em `<li>` marcas. Pode, em seguida, concluir que as pessoas descobriram Olá novo `<li>` marcas são clicáveis e agora está limpando todas as suas tarefas previamente concluídas no aplicativo hello.

Com base nos dados de saudação da sua implantação flighting, você decidir que a nova interface do usuário está pronto para produção.

## <a name="go-live-move-your-new-code-into-production"></a>Ativação: mover seu novo código para a produção
Você está agora pronto toomove tooproduction sua atualização. O grande é que agora você sabe que a atualização já foi validada *antes de* é enviada por push tooproduction. Agora você pode implantá-la com confiança. Desde que você fez um aplicativo de cliente atualização toohello AngularJS, validados somente código de cliente hello. Se você fosse um aplicativo de API da Web de back-end do toomake alterações toohello, você pode validar as alterações da mesma forma e facilmente.

1. No Shell de Git, remova a regra de roteamento de tráfego da saudação executando Olá comando a seguir:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Execute comandos do Git hello:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Aguarde alguns minutos para Olá novos toohello toobe implantado slot de preparo de código, em seguida, inicie http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net que Olá nova atualização aquecido em preparo Olá slot. Lembre-se de que Olá ramificação mestre da bifurcação está vinculado toohello preparo slot do aplicativo.
4. Agora, trocar o slot de preparação para a produção de hello

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Resumo
Serviço de aplicativo do Azure facilita tootest toomedium pequenos negócios seus aplicativos voltados para o cliente em produção, algo que foi feito tradicionalmente em grandes empresas. Esperamos que este tutorial lhe concedeu Olá conhecimento necessário toobring juntos Application Insights e do serviço de aplicativo toomake flighting implantação possíveis e outros cenários de teste em produção, seu mundo DevOps.

## <a name="more-resources"></a>Mais recursos
* [Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure](app-service-agile-software-development.md)
* [Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md)
* [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md)
* [Criando modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Olá validador de JSON](http://jsonlint.com/)
* [Ramificação Git – Conceitos básicos de ramificação e mesclagem](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [PowerShell do Azure](/powershell/azure/overview)
* [Projeto Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
