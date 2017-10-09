<span data-ttu-id="ab194-101">Coleção de medidas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ab194-101">Collection of custom measurements.</span></span> <span data-ttu-id="ab194-102">Use este tooreport coleção chamada de medida associada ao item de telemetria Olá.</span><span class="sxs-lookup"><span data-stu-id="ab194-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="ab194-103">Os casos de uso típicos são:</span><span class="sxs-lookup"><span data-stu-id="ab194-103">Typical use cases are:</span></span>
- <span data-ttu-id="ab194-104">tamanho de saudação da carga de telemetria de dependência</span><span class="sxs-lookup"><span data-stu-id="ab194-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="ab194-105">número de saudação de itens da fila processadas pelo telemetria de solicitação</span><span class="sxs-lookup"><span data-stu-id="ab194-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="ab194-106">tempo de cliente levou toocomplete Olá etapa na conclusão do Assistente de etapa telemetria de evento.</span><span class="sxs-lookup"><span data-stu-id="ab194-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="ab194-107">Você pode consultar [medidas personalizadas](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) na Análise do Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="ab194-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="ab194-108">Medidas personalizadas são associadas a itens de telemetria Olá pertencerem a.</span><span class="sxs-lookup"><span data-stu-id="ab194-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="ab194-109">Eles são toosampling de entidade com o item de telemetria Olá contendo essas medidas.</span><span class="sxs-lookup"><span data-stu-id="ab194-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="ab194-110">uma medida que tem um valor independente de outros tipos de telemetria, uso de tootrack [telemetria de métrica](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ab194-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="ab194-111">Comprimento de chave máximo: 150</span><span class="sxs-lookup"><span data-stu-id="ab194-111">Max key length: 150</span></span>
