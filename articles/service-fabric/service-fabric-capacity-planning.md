---
title: aaaCapacity planejamento para aplicativos do Service Fabric | Microsoft Docs
description: "Descreve como tooidentify Olá número de nós de computação necessários para um aplicativo do Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Planejamento de capacidade para Aplicativos do Service Fabric
Este documento ensina como tooestimate Olá a quantidade de recursos (CPUs, RAM, armazenamento em disco) é necessário toorun seus aplicativos do Azure Service Fabric. É comum para sua toochange de requisitos de recursos ao longo do tempo. Normalmente, você precisa de alguns recursos enquanto desenvolve/testa seu serviço e, posteriormente, precisa de mais recursos à medida que entra na fase de produção e a popularidade de seu aplicativo aumenta. Quando você projetar seu aplicativo, considerar os requisitos de longo prazo hello e fazer escolhas que permitem que a demanda do serviço tooscale toomeet cliente alta.

 Quando você cria um cluster do Service Fabric, você decidir os tipos de máquinas virtuais (VMs) fazer backup de cluster de saudação. Cada VM vem com uma quantidade limitada de recursos na forma de saudação do armazenamento em disco, largura de banda de rede, RAM e CPUs (núcleos e velocidade). À medida que cresce o serviço ao longo do tempo, você pode atualizar tooVMs que oferecem mais recursos de e/ou adicionar mais cluster tooyour de VMs. Olá toodo último, você deverá arquitetar seu serviço inicialmente para que ele pode aproveitar novas VMs que são adicionados dinamicamente o cluster toohello.

Alguns serviços gerenciar poucos dados toono Olá próprias VMs. Portanto, para esses serviços devem se concentrar principalmente em desempenho, o que significa que selecionando Olá de planejamento de capacidade apropriados CPUs (núcleos e velocidade) de saudação VMs. Além disso, você deve considerar a largura de banda da rede, incluindo a frequência das transferências de rede e a quantidade de dados que está sendo transferida. Se seu serviço precisa tooperform bem como o aumento do uso de serviço, você pode adicionar mais cluster de toohello de VMs e carregar solicitações de rede de saudação do saldo em todas as VMs de saudação.

Para serviços que gerenciam grandes quantidades de dados em VMs do hello, planejamento de capacidade deve se concentrar principalmente em tamanho. Assim, você deve considerar atentamente a capacidade de saudação da saudação da VM RAM e armazenamento em disco. sistema de gerenciamento de memória virtual Olá no Windows torna o espaço em disco se parecer com o código de tooapplication de RAM. Além disso, o tempo de execução do Service Fabric Olá fornece mantendo dados ativos somente na memória e toodisk movimentação de dados frios Olá a paginação inteligente. Aplicativos, portanto, podem usar mais memória do que está fisicamente disponível em Olá VM. Simplesmente ter mais RAM aumenta o desempenho, pois Olá VM pode manter mais armazenamento em disco na memória RAM. Olá VM que você selecionar deve ter um dados Olá toostore grande o suficiente de disco que você deseja na Olá VM. Da mesma forma, Olá VM deve ter suficiente tooprovide RAM com hello desempenho desejados. Se os dados do serviço aumentar ao longo do tempo, você pode adicionar mais máquinas virtuais toohello cluster e particionar dados saudação em todas as VMs de saudação.

## <a name="determine-how-many-nodes-you-need"></a>Determinar quantos nós são necessários
Particionamento de seu serviço permite que você tooscale os dados do serviço. Para obter mais informações sobre particionamento, consulte [Particionamento do Service Fabric](service-fabric-concepts-partitioning.md). Cada partição deve se ajustar a uma única VM, mas várias partições (pequenas) podem ser colocadas em uma única VM. Portanto, ter mais partições pequenas fornece maior flexibilidade do que ter poucas partições maiores. compensação de saudação é que ter muitas partições aumenta a sobrecarga de malha do serviço e você não pode executar operações realizadas em partições. Há também mais tráfego de rede potencial se seu código de serviço precisa frequentemente tooaccess partes dos dados que residem em diferentes partições. Ao projetar seu serviço, você deve considerar cuidadosamente esses tooarrive prós e contras em uma estratégia de particionamento eficaz.

Vamos supor que seu aplicativo tem um único serviço com monitoração de estado que tem um tamanho de armazenamento que você espera que toogrow tooDB_Size GB em um ano. Você está disposto tooadd mais aplicativos (e partições) como experiência crescimento além daquele ano.  Olá fator de replicação (FR), que determina o número de saudação de réplicas para seu serviço impactos Olá DB_Size total. Olá que db_size total em todas as réplicas é hello multiplicado por DB_Size de fator de replicação.  Node_Size representa o espaço de disco Olá/RAM por nó, você deseja toouse para seu serviço. Para melhor desempenho, Olá DB_Size deve caber na memória em cluster hello e um Node_Size ao redor Olá RAM de saudação que VM deve ser escolhida. Alocando um Node_Size maior Olá capacidade de RAM, você depender de paginação Olá fornecida pelo tempo de execução do hello Service Fabric. Assim, o desempenho pode não ser ideal se seus dados de inteiros são considerados uma toobe hot (desde a saudação, em seguida, dados são paginados de entrada/saída). No entanto, para muitos serviços onde somente uma fração dos dados saudação está ativa, é mais econômico.

número de saudação de nós necessários para o desempenho máximo pode ser computado da seguinte maneira:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Pense no crescimento
Talvez você queira toocompute número de saudação de nós com base em Olá DB_Size que você espera que seu toogrow de serviço, além de toohello DB_Size que começa com. Em seguida, crescer número Olá de nós à medida que aumenta de seu serviço para que não são provisionamento excessivo número Olá de nós. Mas o número de saudação de partições deve ser com base no número de saudação de nós que são necessárias quando você estiver executando o serviço de no máximo de crescimento.

Ele é bom toohave algumas máquinas adicionais disponíveis a qualquer momento, para que você possa tratar picos inesperados ou a falha (por exemplo, se alguns VMs descem).  Embora Olá capacidade extra deve ser determinada usando seu picos esperados, um ponto de partida é tooreserve algumas VMs adicionais (5-10 por cento extra).

Olá anterior pressupõe um único serviço com monitoração de estado. Se você tiver mais de um serviço com monitoração de estado, você tem tooadd Olá DB_Size associado Olá outros serviços equação hello. Como alternativa, você pode calcular o número de saudação de nós separadamente para cada serviço com monitoração de estado.  O serviço pode ter réplicas ou partições que não são equilibradas. Tenha em mente que as partições também podem ter mais dados do que outras. Para obter mais informações sobre particionamento, consulte [Particionamento de artigo nas práticas recomendadas](service-fabric-concepts-partitioning.md). No entanto, hello equação anterior é partição e réplica desconhecido, porque o Service Fabric garante que réplicas de saudação são distribuídas entre os nós de saudação de forma otimizada.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Use uma planilha para calcular o custo
Agora vamos adicionar alguns números reais fórmula hello. Um [planilha de exemplo](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) mostra como tooplan Olá capacidade para um aplicativo que contém três tipos de objetos de dados. Para cada objeto, podemos aproximar seu tamanho e quantos objetos que esperamos toohave. Também selecionamos quantas réplicas queremos de cada tipo de objeto. planilha de saudação calcula a quantidade total de saudação de memória toobe armazenado no cluster de saudação.

Em seguida, inserimos um tamanho de VM e um custo mensal. Com base no tamanho da VM de saudação, planilha Olá informa que Olá número mínimo de partições, que você deve usar toosplit toophysically seus dados se ajustar em nós de saudação. Pode ser um número maior de partições tooaccommodate que necessidades de tráfego específico de computação e rede do seu aplicativo. planilha de saudação mostra o número de saudação de partições que estão gerenciando objetos de perfil de usuário Olá aumentou de um toosix.

Agora, com base em todas essas informações, planilha Olá mostra que você pode obter todos os dados de saudação com hello desejado partições e réplicas fisicamente em um cluster de nó de 26. No entanto, esse cluster deve ser compactado, portanto algumas falhas de nó tooaccommodate nós adicionais e atualizações. planilha de saudação também mostra que com mais de 57 nós fornece nenhum valor adicional, porque você teria que nós vazios. Novamente, talvez você queira toogo acima 57 nós mesmo assim as falhas de nó tooaccommodate e as atualizações. É possível ajustar a saudação planilha toomatch necessidades específicas do seu aplicativo.   

![Planilha para cálculo de custo][Image1]

## <a name="next-steps"></a>Próximas etapas
Check-out [serviços do Service Fabric particionamento] [ 10] toolearn mais sobre o particionamento de seu serviço.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
