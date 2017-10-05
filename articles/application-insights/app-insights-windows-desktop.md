---
title: "Monitorando uso e desempenho de aplicativos de área de trabalho do Windows"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="734b2-103">Monitorando uso e desempenho de aplicativos de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="734b2-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="734b2-104">[Azure Application Insights](app-insights-overview.md) e [HockeyApp](https://hockeyapp.net) permitem que você monitore seu aplicativo implantado quanto ao uso e desempenho.</span><span class="sxs-lookup"><span data-stu-id="734b2-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="734b2-105">Recomendamos o [HockeyApp](https://hockeyapp.net) para distribuir e monitorar aplicativos de área de trabalho e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="734b2-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="734b2-106">Com o HockeyApp, você pode gerenciar a distribuição, testes ao vivo e comentários do usuário, bem como monitorar relatórios de uso e falhas.</span><span class="sxs-lookup"><span data-stu-id="734b2-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="734b2-107">Você também pode [exportar e consultar a telemetria com o Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="734b2-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="734b2-108">Embora a telemetria possa ser enviada para o Application Insights de um aplicativo de área de trabalho, isso é principalmente útil para fins experimentais e de depuração.</span><span class="sxs-lookup"><span data-stu-id="734b2-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="734b2-109">Para enviar telemetria ao Application Insights de um aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="734b2-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="734b2-110">No [portal do Azure](https://portal.azure.com), [crie um recurso Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="734b2-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="734b2-111">Para o tipo de aplicativo, escolha o aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="734b2-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="734b2-112">Faça uma cópia da chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="734b2-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="734b2-113">Localize a chave no menu suspenso Essentials do novo recurso que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="734b2-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="734b2-114">No Visual Studio, edite os pacotes NuGet do seu projeto de aplicativo e adicione Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="734b2-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="734b2-115">(Ou escolha Microsoft.ApplicationInsights se você quiser apenas a API básica, sem os módulos de coleta da telemetria padrão.)</span><span class="sxs-lookup"><span data-stu-id="734b2-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="734b2-116">Defina a chave de instrumentação no seu código:</span><span class="sxs-lookup"><span data-stu-id="734b2-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="734b2-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *sua chave* `";`</span><span class="sxs-lookup"><span data-stu-id="734b2-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="734b2-118">ou em ApplicationInsights.config (se tiver instalado um dos pacotes de telemetria padrão):</span><span class="sxs-lookup"><span data-stu-id="734b2-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="734b2-119">`<InstrumentationKey>`*sua chave*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="734b2-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="734b2-120">Se você usar ApplicationInsights.config, verifique se suas propriedades no Gerenciador de Soluções estão definidas como **Ação de Compilação = Conteúdo, Copiar para Diretório de Saída = Copiar**.</span><span class="sxs-lookup"><span data-stu-id="734b2-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="734b2-121">[Use a API](app-insights-api-custom-events-metrics.md) para enviar telemetria.</span><span class="sxs-lookup"><span data-stu-id="734b2-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="734b2-122">Execute o aplicativo e veja a telemetria no recurso criado no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="734b2-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="734b2-123"><a name="telemetry"></a>Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="734b2-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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

## <a name="next-steps"></a><span data-ttu-id="734b2-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="734b2-124">Next steps</span></span>
* [<span data-ttu-id="734b2-125">Criar um painel</span><span class="sxs-lookup"><span data-stu-id="734b2-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="734b2-126">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="734b2-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="734b2-127">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="734b2-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="734b2-128">Escrever consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="734b2-128">Write Analytics queries</span></span>](app-insights-analytics.md)

