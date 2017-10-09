Fábrica de dados é um serviço de multilocatário tem Olá limites padrão no lugar toomake-se de que as assinaturas de cliente são protegidas contra umas das outras cargas de trabalho a seguir. Muitos dos limites de saudação podem ser facilmente gerados para sua assinatura, o limite máximo de toohello entrando em contato com o suporte.

| **Recurso** | **Limite padrão** | **Limite máximo** |
| --- | --- | --- |
| data factories em uma assinatura do Azure |50 |[Contate o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| pipelines em um data factory |2500 |[Contate o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| conjuntos de dados em um data factory |5.000 |[Contate o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| fatias simultâneas por conjunto de dados |10 |10 |
| bytes por objeto para objetos do pipeline <sup>1</sup> |200 KB |200 KB |
| bytes por objeto para objetos de conjunto de dados e serviço vinculado <sup>1</sup> |100 KB |2000 KB |
| núcleos de cluster sob demanda HDInsight em uma assinatura <sup>2</sup> |60 |[Contate o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Unidade de movimentação de dados de nuvem <sup>3</sup> |32 |[Contate o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Contagem novas tentativas de execução de atividade do pipeline |1000 |MaxInt (32 bits) |

<sup>1</sup> Objetos de pipeline, conjunto de dados e serviço vinculado representam um agrupamento lógico de sua carga de trabalho. Limites para esses objetos não estão relacionados a tooamount de dados, você pode mover e processar com o serviço do Azure Data Factory hello. Fábrica de dados é projetado tooscale toohandle petabytes de dados.

<sup>2</sup> núcleos HDInsight sob demanda são alocados sem assinatura Olá que contém a fábrica de dados hello. Como resultado, Olá acima do limite é hello fábrica de dados imposta limite de núcleos de HDInsight sob demanda núcleos e é diferente do limite de núcleos Olá associado à sua assinatura do Azure.

<sup>3</sup> A DMU (unidade de movimentação de dados de nuvem) está sendo usada em uma operação de cópia de nuvem para nuvem. É uma medida que representa a potência de saudação (uma combinação de CPU, memória e alocação de recursos de rede) de uma única unidade na fábrica de dados. Você pode obter uma taxa de transferência de cópia mais alta aproveitando mais DMUs em alguns cenários. Consulte também[unidades de movimentação de dados em nuvem](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) seção em detalhes.

| **Recurso** | **Limite inferior padrão** | **Limite mínimo** |
| --- | --- | --- |
| Intervalo de agendamento |15 minutos |15 minutos |
| Intervalo entre novas tentativas |1 segundo |1 segundo |
| Valor de tempo limite de nova tentativa |1 segundo |1 segundo |

### <a name="web-service-call-limits"></a>Limites de chamada de serviço Web
O Azure Resource Manager tem limites para chamadas à API. Você pode fazer chamadas de API em uma taxa de saudação [API do Gerenciador de recursos do Azure limita](../articles/azure-subscription-service-limits.md#resource-group-limits).
