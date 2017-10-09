
>[!NOTE]
>O Log Analytics era conhecido como Operational Insights.
>
>

Olá limites a seguir se aplicam a recursos de análise de tooLog por assinatura:

| Recurso | Limite padrão | Comentários
| --- | --- | --- |
| Número de espaços de trabalho gratuitos por assinatura | 10 | Esse limite não pode ser aumentado. |
| Número de espaços de trabalho pagos por assinatura | N/D | Você está limitado pelo número de saudação de recursos dentro de um grupo de recursos e o número de grupos de recursos por assinatura | 


Olá limites a seguir se aplicam a espaço de trabalho de análise de Log tooeach:

|  | Grátis | Standard | Premium | Autônomo | OMS |
| --- | --- | --- | --- | --- | --- |
| Volume de dados coletado por dia |500 MB<sup>1</sup> |Nenhum |Nenhum | Nenhum | Nenhum
| Período de retenção de dados |7 dias |1 mês |12 meses | 1 mês<sup>2</sup> | 1 mês <sup>2</sup>|

<sup>1</sup> quando os clientes atingir seu limite de transferência de dados diário 500 MB, análise de dados para e reinicia no início de saudação do hello próximo dia. Um dia é baseado em UTC.

<sup>2</sup> período de retenção de dados Olá Olá autônomo e planos de preços do OMS pode ser aumentada too730 dias.

| Categoria | Limites | Comentários
| --- | --- | --- |
| API do Coletor de Dados | O tamanho máximo para uma postagem única é de 30 MB<br>O tamanho máximo para valores de campo é de 32 KB | Dividir volumes maiores em várias postagens<br>Campos com mais de 32 KB são truncados. |
| API de Pesquisa | 5000 registros retornados para dados não agregados<br>500000 registros para os dados agregados | Dados agregados são uma pesquisa que inclui Olá `measure` comando
 
