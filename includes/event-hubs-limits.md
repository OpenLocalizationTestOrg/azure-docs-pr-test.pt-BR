Hello tabela a seguir lista as cotas e limita os Hubs de eventos específico tooAzure. Para saber mais sobre os preços dos Hubs de Eventos, veja os [preços dos Hubs de Eventos](https://azure.microsoft.com/pricing/details/event-hubs/).

| Limite | Escopo | Tipo | Comportamento quando excedido | Valor |
| --- | --- | --- | --- | --- |
| Número de Hubs de Eventos por namespace |Namespace |Estático |As solicitações seguintes para a criação de um novo namespace serão rejeitadas. |10 |
| O número de partições por Hub de Eventos |Entidade |Estático |- |32 |
| Número de grupos de consumidores por Hub de Eventos |Entidade |Estático |- |20 |
| Número de conexões AMQP por namespace |Namespace |estático |As solicitações subsequentes de conexões adicionais serão rejeitadas e uma exceção será recebida pelo Olá chamando código. |5.000 |
| Tamanho máximo de eventos de Hubs de Eventos|Todo o sistema |Estático |- |256 KB |
| Tamanho máximo do nome de um Hub de Eventos |Entidade |Estático |- |50 caracteres |
| Número de destinatários sem época por grupo de consumidores |Entidade |Estático |- |5 |
| Período de retenção máximo dos dados do evento |Entidade |Estático |- |Um a sete dias |
| Unidades de produtividade máxima |Namespace |estático |Limite de unidade de taxa de transferência Olá excedente faz com que o toobe de dados limitada e gera um  **[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)**. Você pode solicitar um número maior de unidades de produtividade para uma camada Standard ao preencher uma [solicitação de suporte](/azure/azure-supportability/how-to-create-azure-support-request). As [unidades de produtividade adicionais](../articles/event-hubs/event-hubs-auto-inflate.md) estão disponíveis em blocos de 20, em uma base de compra garantida. |20 |

