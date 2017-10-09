---
title: "Considerações de desempenho e otimização de pesquisa aaaAzure | Microsoft Docs"
description: Ajustar o desempenho da Pesquisa do Azure e configurar o dimensionamento ideal
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Considerações de desempenho e otimização da Pesquisa do Azure
Uma experiência de pesquisa grande é uma chave toosuccess para muitos móveis e aplicativos da web. De imóveis, catálogos de tooonline tooused carro mercados, a pesquisa rápida e resultados relevantes afetará experiência de saudação do cliente. Este documento é pretendido toohelp descobrir as práticas recomendadas para como Olá tooget máximo proveito de pesquisa do Azure, especialmente para cenários avançados com sofisticadas requisitos de escalabilidade, suporte a vários idiomas ou classificação personalizada.  Além disso, este documento descreve componentes internos e cobre abordagens que funcionam bem em aplicativos reais de clientes.

## <a name="performance-and-scale-tuning-for-search-services"></a>Ajuste de desempenho e escala para serviços de pesquisa
Estamos todos os mecanismos de toosearch usado como o Bing e Google e saudação de alto desempenho que oferecem.  Como resultado, quando os clientes usam seu aplicativo móvel ou da Web habilitado para pesquisa, eles esperam características de desempenho semelhantes.  Quando a otimização de desempenho da pesquisa, uma das abordagens recomendadas Olá é toofocus na latência, que é Olá tempo uma consulta toocomplete e retornar resultados.  Ao otimização a latência de pesquisa é importante:

1. Escolha uma latência de destino (ou a quantidade máxima de tempo) que uma solicitação de pesquisa típica deve levar toocomplete.
2. Criar e testar uma carga de trabalho real em relação a seu serviço de pesquisa com um conjunto de dados realista toomeasure essas taxas de latência.
3. Iniciar com um número baixo de consultas por segundo (QPS) e continue o número de saudação tooincrease executado no teste de saudação até que a consulta Olá latência está abaixo da saudação definido latência de destino.  Este é um toohelp benchmark importante que você planeje a expansão à medida que aumenta de seu aplicativo em uso.
4. Sempre que possível, reutilize as conexões HTTP.  Se você estiver usando Olá SDK .NET da pesquisa do Azure, isso significa que você deve reutilizar uma instância ou [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) de instância e se você estiver usando Olá API REST, você deve reutilizar um único HttpClient.

Ao criar essas cargas de trabalho de teste, há algumas características de pesquisa do Azure tookeep em mente:

1. É possível toopush muitas consultas feitas ao mesmo tempo, que recursos de saudação disponíveis em seu serviço de pesquisa do Azure serão sobrecarregados.  Quando isso acontecer, você verá códigos de resposta HTTP 503.  Por esse motivo, é melhor toostart com vários intervalos de pesquisa solicitações toosee Olá diferenças em taxas de latência conforme você adiciona mais solicitações de pesquisa.
2. Carregamento de conteúdo tooAzure pesquisa afetará Olá desempenho geral e latência de Olá serviço de pesquisa do Azure.  Se você espera que os dados de toosend enquanto os usuários estão fazendo pesquisas, é importante tootake essa carga de trabalho na conta em seus testes.
3. Nem todas as consultas de pesquisa executará em Olá mesmo níveis de desempenho.  Por exemplo, uma sugestão de pesquisa ou pesquisa de documento normalmente será executada mais rápido do que uma consulta com um número considerável de facetas e filtros.  É melhor Olá tootake várias consultas que você espera toosee em conta ao criar seus testes.  
4. Variação de solicitações de pesquisa é importante porque, se você executar continuamente Olá mesmo solicitações de pesquisa, o cache de dados inicial toomake desempenho ficará melhor que ele pode com uma consulta mais diferentes definido.

> [!NOTE]
> [Teste de carga do Visual Studio](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) é tooperform uma maneira muito bom seu parâmetro de comparação testes que permite a você solicitações tooexecute HTTP que seria necessário para executar consultas em relação a pesquisa do Azure e habilita a paralelização de solicitações.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Dimensionamento da Pesquisa do Azure para taxas de consulta altas e solicitações limitadas
Quando você está recebendo muitas solicitações limitadas ou excede suas taxas de latência de destino de uma carga maior de consulta, você pode examinar as taxas de latência de toodecrease de duas maneiras:

1. **Réplicas de aumento:** uma réplica é semelhante a uma cópia de dados permitir solicitações de saldo de tooload de pesquisa do Azure em relação a saudação várias cópias.  Todos o balanceamento de carga e a replicação de dados por meio de réplicas é gerenciada pela pesquisa do Azure e você pode alterar o número de saudação de réplicas alocada para o serviço a qualquer momento.  Você pode alocar too12 réplicas em um serviço de pesquisa padrão e 3 réplicas em um serviço de pesquisa básica. As réplicas podem ser ajustadas de saudação [portal do Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).
2. **Aumentar a Camada de Pesquisa:** o Azure Search vem em [várias camadas](https://azure.microsoft.com/pricing/details/search/), e cada uma dessas camadas oferece níveis diferentes de desempenho.  Em alguns casos, você pode ter muitas consultas nessa camada Olá em que estão não pode fornecer taxas suficientemente baixa latência, mesmo quando réplicas são maximizadas.  Nesse caso, convém tooconsider aproveitar um dos níveis mais altos de pesquisa hello como camada de S3 de pesquisa do Azure Olá que é adequado para cenários com um grande número de documentos e cargas de trabalho de consulta muito alta.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Dimensionamento da Pesquisa do Azure para consultas individuais lentas
Outro motivo por que as taxas de latência podem ser lentas é de uma única consulta demorando muito toocomplete.  Nesse caso, a adição de réplicas não melhorará as taxas de latência.  Para esses casos, há duas opções disponíveis:

1. **Aumentar Partições** Uma partição é um mecanismo para dividir os dados entre recursos extras.  Por esse motivo, quando você adiciona uma segunda partição, seus dados são divididos em dois.  Uma terceira partição divide o índice em três etc.  Isso também tem o efeito de saudação que em alguns casos, consultas lentas executará mais rápido devido a paralelização toohello de computação.  Há alguns exemplos nos quais temos visto essa paralelização funcionar muito bem com consultas de baixa seletividade.  Isso consiste em consultas que corresponder a vários documentos ou quando as necessidades de facetas tooprovide contagens de grandes números de documentos.  Como há que um lote de computação necessária tooscore relevância de saudação de documentos de saudação ou números de saudação toocount de documentos, adicionando partições adicionais podem ajudar a computação adicionais tooprovide.  
   
   Pode haver um máximo de 12 partições no serviço de pesquisa padrão e 1 partição no serviço de pesquisa básica hello.  As partições podem ser ajustadas de saudação [portal do Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).
2. **Campos de cardinalidade alto limite:** um campo de alta cardinalidade consiste em uma facetable ou podem ser filtrado campo que tem um número significativo de valores exclusivos e como resultado, assume muitos recursos toocompute resultados.   Por exemplo, a configuração de um campo de descrição ou a identificação de produto como facetable/filtrável faria para alta cardinalidade porque a maioria dos valores de saudação do documento toodocument é exclusiva. Sempre que possível, limitar o número de saudação de campos de alta cardinalidade.
3. **Camada de pesquisa de aumento:** subindo tooa mais alto nível de pesquisa do Azure pode ser outro desempenho tooimprove de maneira de consultas lentas.  Cada camada superior também fornece uma CPU mais rápida e mais memória, o que pode ter um impacto positivo no desempenho da consulta.

## <a name="scaling-for-availability"></a>Dimensionamento para disponibilidade
As réplicas não apenas ajudam a reduzir a latência da consulta, mas também permitem a alta disponibilidade.  Com uma única réplica, você deve esperar o tempo de inatividade periódico devido tooserver reinicializações após as atualizações de software ou de outros eventos de manutenção que ocorrerão.  Como resultado, é importante tooconsider se seu aplicativo exigir alta disponibilidade de pesquisas (consultas), bem como gravações (eventos de indexação).  A pesquisa do Azure oferece opções de SLA em todos os Olá ofertas de pesquisa paga por hello seguintes atributos:

* Duas réplicas para alta disponibilidade das cargas de trabalho somente leitura (consultas)
* Três ou mais réplicas para alta disponibilidade das cargas de trabalho de leitura/gravação (consultas e indexação)

Para obter mais detalhes sobre isso, visite Olá [contrato de nível de serviço de pesquisa do Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Desde que as réplicas são cópias de seus dados, com várias réplicas permite que a pesquisa do Azure toodo máquina reinicializações e manutenção com base em uma réplica em um momento enquanto permite que consultas toobe toocontinue executada em Olá outras réplicas.  Por esse motivo, você também precisará tooconsider como esse tempo de inatividade pode impactar consultas Olá que agora têm toobe executado em um menor cópia dos dados de saudação.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Dimensionamento de cargas de trabalho distribuídas geograficamente e fornecimento de redundância geográfica
Para cargas de trabalho distribuído geograficamente, você descobrirá que os usuários localizados distantes Olá data center em que o serviço de pesquisa do Azure é hospedado terá taxas mais altas de latência.  Por esse motivo, é geralmente importante toohave pesquisa vários serviços em regiões que estão em usuários de toothese proximidade mais próximos.  A pesquisa do Azure atualmente não fornece um método automatizado de replicação geográfica índices de pesquisa do Azure entre regiões, mas há algumas técnicas que podem ser usadas que podem gerenciar e fazer essa tooimplement simples do processo. Elas são descritas na Olá próximas seções.

meta de um conjunto distribuído geograficamente de serviços de pesquisa Hello é toohave dois ou mais índices disponíveis em duas ou mais regiões em que o usuário será roteado toohello serviço de pesquisa do Azure que fornece a latência mais baixa hello como mostrado neste exemplo:

   ![Tabela de referência cruzada de serviços por região][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Manter os dados sincronizados em vários serviços de Pesquisa do Azure
Há duas opções para manter seus serviços de pesquisa distribuída em sincronia que consistem em usando Olá [indexador da pesquisa do Azure](search-indexer-overview.md) ou Olá API Push (também chamado hello tooas [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indexadores na Pesquisa do Azure
Se você estiver usando Olá indexador da pesquisa do Azure, você já estiver importando as alterações de dados de um repositório central de dados como banco de dados do Azure SQL ou banco de dados do Azure Cosmos. Quando você cria uma nova pesquisa serviço, você simplesmente também criar um novo indexador da pesquisa do Azure para o serviço que toothis pontos mesmo repositório de dados. Dessa forma, sempre que novas alterações entram em armazenamento de dados hello, elas serão indexados por Olá vários indexadores.  

Veja um exemplo de como seria a aparência dessa arquitetura.

   ![Única fonte de dados com o indexador distribuído e combinações de serviço][2]

### <a name="push-api"></a>API Push
Se você estiver usando Olá Push API de pesquisa do Azure muito[atualizar conteúdo em seu índice de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/update-index), você pode manter seus vários serviços de pesquisa em sincronia Enviando alterações tooall pesquisa serviços sempre que uma atualização é necessária.  Quando isso é importante toomake se toohandle casos em que um serviço de pesquisa de tooone de atualização falha e bem-sucedida de uma ou mais atualizações.

## <a name="leveraging-azure-traffic-manager"></a>Aproveitando o Gerenciador de Tráfego do Azure
[O Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) permite que você tooroute solicitações toomultiple localizados geograficamente sites que, em seguida, são feitos por vários serviços de pesquisa do Azure.  Uma vantagem de saudação do Traffic Manager é que ele pode investigação tooensure de pesquisa do Azure que está disponível e rotear os serviços de pesquisa tooalternate usuários no evento de saudação do tempo de inatividade.  Além disso, se você está roteando as solicitações de pesquisa por meio de Sites do Azure, o Azure Traffic Manager permite casos de saldo de tooload onde Olá site está ativo, mas não a pesquisa do Azure.  Aqui está um exemplo de arquitetura que Olá que utiliza o Gerenciador de tráfego.

   ![Tabela de referência cruzada de serviços por região, com o Gerenciador de tráfego central][3]

## <a name="monitoring-performance"></a>Monitoramento de desempenho
A pesquisa do Azure oferece Olá capacidade tooanalyze Olá desempenho do monitor do serviço por meio de [análise de tráfego de pesquisa (STA)](search-traffic-analytics.md). Por meio de STA, você pode, opcionalmente, registrar as operações de pesquisa individual Olá assim como uma conta de armazenamento do Azure de tooan as métricas agregadas que pode ser processada para análise ou visualizada no Power BI.  Usando as métricas de STA, você pode examinar as estatísticas de desempenho, como o número médio de consultas ou tempos de resposta da consulta.  Além disso, o log de operações Olá permite-lhe toodrill em detalhes das operações de pesquisa específico.

STA é taxas de latência de toounderstand uma ferramenta valiosa sob essa perspectiva de pesquisa do Azure.  Como métricas de desempenho de consulta Olá conectadas se baseiam no tempo de saudação toobe totalmente processada na pesquisa do Azure (do tempo de saudação é toowhen solicitada, ela é enviada) entra em uma consulta, será capaz de toouse este toodetermine se houver problemas de latência de saudação serviço de pesquisa do Azure lado ou fora do hello serviço, como a latência de rede.  

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre Olá preços camadas e os limites de serviços para cada um, consulte [limites na pesquisa do Azure do serviço](search-limits-quotas-capacity.md).

Visite [planejamento de capacidade](search-capacity-planning.md) toolearn mais sobre as combinações de partição e de réplica.

Para mais detalhados sobre desempenho e toosee algumas demonstrações de como tooimplement Olá otimizações discutidas neste artigo, assista a saudação de vídeo a seguir:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
