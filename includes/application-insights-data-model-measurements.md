Coleção de medidas personalizadas. Use este tooreport coleção chamada de medida associada ao item de telemetria Olá. Os casos de uso típicos são:
- tamanho de saudação da carga de telemetria de dependência
- número de saudação de itens da fila processadas pelo telemetria de solicitação
- tempo de cliente levou toocomplete Olá etapa na conclusão do Assistente de etapa telemetria de evento.

Você pode consultar [medidas personalizadas](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) na Análise do Aplicativo:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Medidas personalizadas são associadas a itens de telemetria Olá pertencerem a. Eles são toosampling de entidade com o item de telemetria Olá contendo essas medidas. uma medida que tem um valor independente de outros tipos de telemetria, uso de tootrack [telemetria de métrica](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Comprimento de chave máximo: 150
