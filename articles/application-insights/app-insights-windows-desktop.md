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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="94b0e-103">Monitorando uso e desempenho de aplicativos de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="94b0e-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="94b0e-104">[Azure Application Insights](app-insights-overview.md) e [HockeyApp](https://hockeyapp.net) permitem que você monitore seu aplicativo implantado quanto ao uso e desempenho.</span><span class="sxs-lookup"><span data-stu-id="94b0e-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94b0e-105">É recomendável [HockeyApp](https://hockeyapp.net) toodistribute e monitorar aplicativos de área de trabalho e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="94b0e-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="94b0e-106">Com o HockeyApp, você pode gerenciar a distribuição, testes ao vivo e comentários do usuário, bem como monitorar relatórios de uso e falhas.</span><span class="sxs-lookup"><span data-stu-id="94b0e-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="94b0e-107">Você também pode [exportar e consultar a telemetria com o Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="94b0e-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="94b0e-108">Embora possa ser enviada a telemetria tooApplication Insights em um aplicativo de área de trabalho, isso é principalmente útil para fins de depuração e experimentais.</span><span class="sxs-lookup"><span data-stu-id="94b0e-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="94b0e-109">toosend telemetria tooApplication Insights de um aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="94b0e-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="94b0e-110">Em Olá [portal do Azure](https://portal.azure.com), [criar um recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="94b0e-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="94b0e-111">Para o tipo de aplicativo, escolha o aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="94b0e-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="94b0e-112">Faça uma cópia da chave de instrumentação de saudação.</span><span class="sxs-lookup"><span data-stu-id="94b0e-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="94b0e-113">Localize chave Olá no hello Essentials lista suspensa do novo recurso de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="94b0e-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="94b0e-114">No Visual Studio, edite pacotes do NuGet saudação do projeto do aplicativo e adicione Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="94b0e-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="94b0e-115">(Ou escolha Microsoft.ApplicationInsights se você quiser apenas Olá API vazio, sem módulos de coleção de telemetria padrão hello.)</span><span class="sxs-lookup"><span data-stu-id="94b0e-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="94b0e-116">Defina chave de instrumentação Olá no seu código:</span><span class="sxs-lookup"><span data-stu-id="94b0e-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="94b0e-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";`</span><span class="sxs-lookup"><span data-stu-id="94b0e-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="94b0e-118">ou no applicationinsights. config (se tiver instalado um dos pacotes de telemetria padrão Olá):</span><span class="sxs-lookup"><span data-stu-id="94b0e-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="94b0e-119">`<InstrumentationKey>`*sua chave*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="94b0e-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="94b0e-120">Se você usar applicationinsights. config, verifique se suas propriedades no Gerenciador de soluções estão definidas muito**Build Action = conteúdo, cópia tooOutput Directory = copiar**.</span><span class="sxs-lookup"><span data-stu-id="94b0e-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="94b0e-121">[Use a API de saudação](app-insights-api-custom-events-metrics.md) toosend telemetria.</span><span class="sxs-lookup"><span data-stu-id="94b0e-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="94b0e-122">Executar seu aplicativo e ver a telemetria Olá no recurso Olá criado no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="94b0e-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="94b0e-123"><a name="telemetry"></a>Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="94b0e-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="94b0e-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94b0e-124">Next steps</span></span>
* [<span data-ttu-id="94b0e-125">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="94b0e-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="94b0e-126">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="94b0e-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="94b0e-127">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="94b0e-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="94b0e-128">Escrever consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="94b0e-128">Write Analytics queries</span></span>](app-insights-analytics.md)

