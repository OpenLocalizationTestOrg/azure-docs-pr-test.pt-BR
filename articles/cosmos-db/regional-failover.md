---
title: aaaRegional failover no banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como o failover manual e automáticos funcionam com o Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Failover regional automático para a continuidade dos negócios no Azure Cosmos DB
Banco de dados do Azure Cosmos simplifica a distribuição global Olá de dados, oferecendo totalmente gerenciado, [contas de banco de dados de várias regiões](distribute-data-globally.md) que fornecem limpar compensações entre consistência, disponibilidade e desempenho, todos com correspondente garantia. Contas do cosmos DB oferecem alta disponibilidade, as latências de dígito único ms, [níveis de consistência bem definidos](consistency-levels.md), transparent failover regional com APIs de hospedagem múltipla e a taxa de transferência da escala tooelastically Olá capacidade e armazenamento globo hello. 

Cosmos DB suporta explícita e failovers baseado em políticas que permitem que você o comportamento de sistema de ponta a ponta de saudação toocontrol no evento de saudação de falhas. Neste artigo, veremos:

* Como funcionam os failovers manuais no Cosmos DB?
* Como funcionam os failovers automáticos no Cosmos DB e o que acontece quando um data center fica indisponível?
* Como você pode usar failovers manuais em arquiteturas de aplicativo?

Saiba mais sobre failovers regionais nesse vídeo do Azure Friday com Scott Hanselman e o gerente de engenharia Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Configurando aplicativos de várias regiões
Antes de mergulhar em modos de failover, vamos examinar como você pode configurar uma vantagem de tootake do aplicativo de várias regiões de disponibilidade e ser resiliente em face de saudação de failovers regional.

* Primeiro, implante seu aplicativo em várias regiões
* acesso de baixa latência tooensure de cada região de seu aplicativo é implantado, configurar Olá correspondente [lista de regiões preferenciais](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) para SDKs com suporte em cada região por meio de uma saudação.

Olá trecho a seguir mostra como tooinitialize um aplicativo de várias regiões. Olá aqui, a conta de banco de dados do Azure Cosmos `contoso.documents.azure.com` é configurado com duas regiões - Oeste dos EUA e Norte da Europa. 

* aplicativo Hello é implantado na região Oeste dos EUA de saudação (por exemplo usando serviços de aplicativo do Azure) 
* Configurado com `West US` como Olá primeiro a região preferida para baixa latência lê
* Configurado com `North Europe` como Olá segundo a região preferida (para alta disponibilidade durante falhas regionais)

Em Olá API DocumentDB, essa configuração é semelhante Olá trecho de código a seguir:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

aplicativo Hello também é implantado na região do Norte da Europa Olá com ordem de saudação das regiões preferenciais revertida. Ou seja, a região do Norte da Europa Olá é especificada primeiro para leituras de baixa latência. Em seguida, região Oeste dos EUA de saudação é especificado como Olá segundo a região preferida para alta disponibilidade durante falhas regionais.

Olá arquitetura diagrama a seguir mostra uma implantação de aplicativo de várias regiões onde o banco de dados do Cosmos e aplicativo hello são toobe configurado em quatro regiões geográficas do Azure.  

![Implantação de aplicativos globalmente distribuídos com o Azure Cosmos DB](./media/regional-failover/app-deployment.png)

Agora, vamos examinar como Olá serviço Cosmos DB trata regionais falhas por meio de failovers automáticos. 

## <a id="AutomaticFailovers"></a>Failovers Automáticos
No evento raro de saudação de uma interrupção regional do Azure ou paralisação do data center, Cosmos DB acionará automaticamente failovers de todas as contas de banco de dados do Cosmos com uma presença na região Olá afetado. 

**O que acontece se uma região de leitura sofre uma interrupção?**

Contas de cosmos banco de dados com uma região de leitura em uma das regiões Olá afetado são automaticamente desconectadas de sua região de gravação e marcado como offline. Olá Cosmos DB SDKs implementar um protocolo de descoberta regionais que lhes permite tooautomatically detectar quando uma região está disponível e chamadas toohello próxima região disponível na lista de região preferida Olá de leitura de redirecionamento. Se nenhuma das regiões Olá Olá região lista preferencial está disponível, chamadas automaticamente recorrer toohello região de gravação atual. Nenhuma alteração é necessária em seu failovers regional do toohandle de código de aplicativo. Durante todo esse processo, garantias de consistência continuam toobe respeitada por banco de dados do Cosmos.

![Falhas de região de leitura no Azure Cosmos DB](./media/regional-failover/read-region-failures.png)

Depois que a região Olá afetado recupera queda de hello, todas as contas de banco de dados do Cosmos Olá afetado na região de saudação são recuperadas automaticamente pelo serviço de saudação. Contas de cosmos banco de dados que tiveram uma região de leitura na região Olá afetado serão e automaticamente sincronizar com a região atual de gravação e ativar online. Olá Cosmos DB SDKs disponibilidade Olá da nova região de saudação de descobrir e avaliar se região Olá deve ser selecionado como Olá leitura a região atual com base na lista de região preferida Olá configurada pelo aplicativo hello. Leituras subsequentes são redirecionadas toohello de região recuperado sem a necessidade de qualquer código de aplicativo tooyour alterações.

**O que acontece se uma região de gravação sofre uma interrupção?**

Se Olá afetados Olá atual gravação região é para uma determinada conta de banco de dados do Cosmos, em seguida, região Olá será automaticamente marcado como offline. Em seguida, uma região alternativa é promovida como Olá gravar região de cada conta de banco de dados do Cosmos afetada. Você pode controlar totalmente a ordem de seleção de região Olá para suas contas de banco de dados do Cosmos via Olá portal do Azure ou [programaticamente](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Prioridades de failover para o Azure Cosmos DB](./media/regional-failover/failover-priorities.png)

Durante failovers automáticos, Cosmos DB escolhe automaticamente Olá a próxima área de gravação para um determinado banco de dados do Cosmos com base em Olá a conta especificada de ordem de prioridade. 

![Falhas de região de gravação no Azure Cosmos DB](./media/regional-failover/write-region-failures.png)

Depois que a região Olá afetado recupera queda de hello, todas as contas de banco de dados do Cosmos Olá afetado na região de saudação são recuperadas automaticamente pelo serviço de saudação. 

* Contas do cosmos banco de dados com sua região de gravação anterior na região Olá afetado permanecerão em modo offline com disponibilidade leitura mesmo após a recuperação de saudação da região de saudação. 
* Você pode consultar toocompute esta região não replicadas gravações durante a interrupção de saudação comparando com dados Olá disponíveis na região de gravação atual hello. Com base nas necessidades de saudação do seu aplicativo, você pode executar a resolução de mesclagem e/ou em conflito e gravar o conjunto final de saudação da região de gravação alterações toohello back atual. 
* Depois de concluir as alterações de mesclagem, você pode colocar região Olá afetado novamente online, removendo e lendo a conta de banco de dados do Cosmos Olá região tooyour. Depois que a região de saudação é adicionado novamente, você pode configurá-lo novamente como região de gravação da saudação executando um failover manual por meio do portal do Azure de saudação ou [programaticamente](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>Failovers Manuais

Além disso, tooautomatic failovers, Olá atual gravar região de uma determinada conta de banco de dados do Cosmos pode ser alterado manualmente dinamicamente tooone de saudação regiões de leitura existente. Failovers manuais podem ser iniciadas por meio do portal do Azure de saudação ou [programaticamente](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Certifique-se de failovers manuais **zero perda de dados** e **zero disponibilidade** perda e normalmente o status de gravação de transferência da saudação antiga gravam região toohello novo da saudação especificou a conta de banco de dados do Cosmos. Como em failovers automáticos, Olá Cosmos DB SDK automaticamente identificadores de gravar as alterações durante failovers manuais de região e garante que as chamadas são toohello automaticamente redirecionado a nova região de gravação. Nenhuma alteração de configuração ou código é necessários em failovers de toomanage seu aplicativo. 

![Failovers manuais no Azure Cosmos DB](./media/regional-failover/manual-failovers.png)

Estes são alguns cenários comuns de saudação em que o failover manual pode ser útil:

**Siga o modelo de relógio Olá**: se seus aplicativos tenham padrões de tráfego previsível com base no tempo de saudação do dia hello, você pode alterar periodicamente Olá gravação status toohello mais ativo região geográfica com base na hora do dia de saudação.

**Atualização de serviço**: determinada implantação de aplicativo distribuído globalmente pode envolver a região de toodifferent tráfego por meio do Gerenciador de tráfego de redirecionamento durante a atualização de serviço planejada. Essa implantação de aplicativo agora pode usar failover manual tookeep Olá gravação status toohello região em que haverá tráfego active toobe durante o período de atualização do serviço de saudação.

**Simulações de BCDR (continuidade dos negócios e recuperação de desastre) e HADR (Alta disponibilidade e recuperação de desastres)**: a maioria dos aplicativos empresariais incluem testes de continuidade de negócios como parte do seu processo de desenvolvimento e lançamento. BCDR e HADR teste geralmente é uma etapa importante em certificações de conformidade e garante disponibilidade de serviço no caso de saudação de interrupções regionais. Você pode testar a preparação BCDR Olá dos aplicativos que usam o banco de dados do Cosmos para armazenamento disparar um failover manual de sua conta de banco de dados do Cosmos e/ou adicionando e removendo uma região dinamicamente.

Neste artigo, analisamos o trabalho de failovers como manual e automática no banco de dados do Cosmos e como você pode configurar seu globalmente disponíveis de toobe Cosmos DB contas e os aplicativos. Ao usar o suporte de replicação global do banco de dados Cosmos, você pode melhorar a latência de ponta a ponta e garantir que eles sejam altamente disponíveis, mesmo em caso de saudação de falhas de região. 

## <a id="NextSteps"></a>Próximas etapas
* Saiba mais sobre como o Cosmos DB dá suporte à [distribuição global](distribute-data-globally.md)
* Saiba mais sobre [consistência global com o Azure Cosmos DB](consistency-levels.md)
* Desenvolver com várias regiões usando o [API do DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md) do Azure Cosmos DB
* Saiba como toobuild [arquiteturas de gravador de várias regiões](multi-region-writers.md) com documentos do Azure

