---
title: "uso de aaaMonitoring e desempenho para aplicativos de área de trabalho do Windows"
description: "Analise o uso e o desempenho do seu aplicativo da área de trabalho do Windows usando o HockeyApp e o Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Monitorando uso e desempenho de aplicativos de área de trabalho do Windows


[Azure Application Insights](app-insights-overview.md) e [HockeyApp](https://hockeyapp.net) permitem que você monitore seu aplicativo implantado quanto ao uso e desempenho.

> [!IMPORTANT]
> É recomendável [HockeyApp](https://hockeyapp.net) toodistribute e monitorar aplicativos de área de trabalho e dispositivo. Com o HockeyApp, você pode gerenciar a distribuição, testes ao vivo e comentários do usuário, bem como monitorar relatórios de uso e falhas. Você também pode [exportar e consultar a telemetria com o Analytics](app-insights-hockeyapp-bridge-app.md).
> 
> Embora possa ser enviada a telemetria tooApplication Insights em um aplicativo de área de trabalho, isso é principalmente útil para fins de depuração e experimentais.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetria tooApplication Insights de um aplicativo do Windows
1. Em Olá [portal do Azure](https://portal.azure.com), [criar um recurso do Application Insights](app-insights-create-new-resource.md). Para o tipo de aplicativo, escolha o aplicativo ASP.NET.
2. Faça uma cópia da chave de instrumentação de saudação. Localize chave Olá no hello Essentials lista suspensa do novo recurso de saudação que você acabou de criar. 
3. No Visual Studio, edite pacotes do NuGet saudação do projeto do aplicativo e adicione Microsoft.ApplicationInsights.WindowsServer. (Ou escolha Microsoft.ApplicationInsights se você quiser apenas Olá API vazio, sem módulos de coleção de telemetria padrão hello.)
4. Defina chave de instrumentação Olá no seu código:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";` 
   
    ou no applicationinsights. config (se tiver instalado um dos pacotes de telemetria padrão Olá):
   
    `<InstrumentationKey>`*sua chave*`</InstrumentationKey>` 
   
    Se você usar applicationinsights. config, verifique se suas propriedades no Gerenciador de soluções estão definidas muito**Build Action = conteúdo, cópia tooOutput Directory = copiar**.
5. [Use a API de saudação](app-insights-api-custom-events-metrics.md) toosend telemetria.
6. Executar seu aplicativo e ver a telemetria Olá no recurso Olá criado no hello Portal do Azure.

## <a name="telemetry"></a>Código de exemplo
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>Próximas etapas
* [Criar um painel](app-insights-dashboards.md)
* [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md)
* [Explorar métricas](app-insights-metrics-explorer.md)
* [Escrever consultas do Analytics](app-insights-analytics.md)

