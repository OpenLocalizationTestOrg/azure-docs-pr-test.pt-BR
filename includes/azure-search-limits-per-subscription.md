Você pode criar vários serviços em uma assinatura, cada um deles configurado em uma camada específica, limitada somente pelo número de saudação de serviços permitidos em cada camada. Por exemplo, você pode criar os serviços de too12 na camada básica hello e 12 outro serviços na camada de saudação S1 em Olá mesmo assinatura. Para obter mais informações sobre as camadas, confira [Escolher uma camada ou SKU para o Azure Search](../articles/search/search-sku-tier.md).

Os limites de serviço máximos podem ser aumentados mediante solicitação. Contate o suporte do Azure se precisar de mais serviços em Olá mesma assinatura.

| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD <sup>1</sup> |
| --- | --- | --- | --- | --- | --- | --- |
| Quantidade máxima de serviços |1 |12 |12 |6 |6 |6 |
| SU de redução horizontal máxima <sup>2</sup> |N/D <sup>3</sup> |3 SU <sup>4</sup> |36 SU |36 SU |36 SU |36 SU |

<sup>1</sup> S3 HD não oferece suporte a [indexadores](../articles/search/search-indexer-overview.md) no momento. 

<sup>2</sup> As SU (unidades de pesquisa) são unidades faturáveis, alocadas como uma *réplica* ou como uma *partição*. Você precisa de ambos de recursos para as operações de armazenamento, indexação e consulta. toolearn mais sobre como as unidades de pesquisa são computadas, além de um gráfico de combinações válidas que permanecem em limites máximos hello, consulte [dimensionar os níveis de recursos para cargas de trabalho de consulta e índice](../articles/search/search-capacity-planning.md). 

<sup>3</sup> Gratuito é baseado nos recursos compartilhados usados por vários assinantes. Neste nível, não há nenhum recurso dedicado para um assinante individual. Por esse motivo, a escala máxima é marcada como não aplicável.

<sup>4</sup> Básica tem uma partição fixa. Nesse nível, SUs adicionais são usadas para alocar mais réplicas para cargas de trabalho de consulta maior.

