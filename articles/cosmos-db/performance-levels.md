---
title: "níveis de desempenho aaaDocumentDB API | Microsoft Docs"
description: "Saiba mais sobre como os níveis de desempenho de API DocumentDB habilitar tooreserve a taxa de transferência em uma base por contêiner."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Desativar Olá S1, S2 e S3 níveis de desempenho

> [!IMPORTANT] 
> Olá S1, S2 e S3 níveis de desempenho discutidos neste artigo estão sendo descartados e não estão mais disponíveis para novas contas de API do DocumentDB.
>

Este artigo fornece uma visão geral dos níveis de desempenho S1, S2 e S3 e discute como coleções de saudação que usam esses níveis de desempenho serão migrados toosingle partição coleções em 1º de agosto de 2017. Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:

- [Por que são desempenho de S1, S2 e S3 Olá níveis desativada?](#why-retired)
- [Como se as coleções de partição única e particionado comparam toohello S1, S2, níveis de desempenho S3?](#compare)
- [O que fazer precisará toodo tooensure ininterrupto acesso toomy dados?](#uninterrupted-access)
- [Como Minha coleção será alterado após a migração Olá?](#collection-change)
- [Como minha cobrança será alterado depois que estou toosingle migrados partição coleções?](#billing-change)
- [E se eu precisar de mais de 10 GB de armazenamento?](#more-storage-needed)
- [Alterar entre níveis de desempenho S1, S2 e S3 de saudação antes de 1 de agosto de 2017?](#change-before)
- [Como saberei quando minha coleção migrou?](#when-migrated)
- [Como migrar do hello S1, S2, S3 desempenho níveis toosingle coleções com uma partição por conta própria?](#migrate-diy)
- [Como serei afetado se eu for um cliente EA?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Por que são desempenho de S1, S2 e S3 Olá níveis desativada?

níveis de desempenho S1, S2 e S3 Olá não oferece flexibilidade de saudação que oferece as coleções de API do DocumentDB. Com hello S1, S2, S3 níveis de desempenho, capacidade Olá taxa de transferência e armazenamento foram predefinida e não oferecia elasticidade. Banco de dados do Azure Cosmos agora fornece Olá capacidade toocustomize sua taxa de transferência e armazenamento, oferece muito mais flexibilidade tooscale sua capacidade de suas necessidades.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Como se as coleções de partição única e particionado comparam toohello S1, S2, níveis de desempenho S3?

Olá, a tabela a seguir compara Olá taxa de transferência e armazenamento opções disponíveis em coleções com uma única partição, coleções particionadas e S1, S2, níveis de desempenho S3. Aqui está um exemplo para a região no Leste dos EUA 2:

|   |Coleção particionada|Coleção de partição única|S1|S2|S3|
|---|---|---|---|---|---|
|Taxa de transferência máxima|Ilimitado|10 K RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Taxa de transferência mínima|2.5 K RU/s|400 RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Armazenamento máximo|Ilimitado|10 GB|10 GB|10 GB|10 GB|
|Preço (mensal)|Taxa de transferência: $ 6/100 RU/s<br><br>Armazenamento: $ 0,25/GB|Taxa de transferência: $ 6/100 RU/s<br><br>Armazenamento: $ 0,25/GB|$ 25 dólares americanos|$ 50 dólares americanos|$ 100 dólares americanos|

Você é um cliente EA? Se for, consulte [Como serei afetado se eu for um cliente EA?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>O que fazer precisará toodo tooensure ininterrupto acesso toomy dados?

Nada, Cosmos DB lida com a migração de saudação para você. Se você tiver uma coleção de S1, S2 ou S3, a coleção atual será migrado tooa partição única coleção em 31 de julho de 2017. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Como Minha coleção será alterado após a migração Olá?

Se você tiver uma coleção de S1, será migrado tooa partição única coleção com taxa de transferência de 400 RU/s. 400 RU/s é hello mais baixa taxa de transferência disponível com coleções com uma única partição. No entanto, custo de saudação de 400 RU/s Olá coleção uma única partição é aproximadamente Olá mesmo que você foram pagar com sua coleção de S1 e 250 RU/s – para que você não estiver pagando Olá extra 150 tooyou disponíveis de RU/s.

Se você tiver uma coleção de S2, será migrado tooa partição única coleção com o 1 K RU/s. Você não verá nenhum nível de taxa de transferência de tooyour de alteração.

Se você tiver uma coleção de S3, será migrado tooa partição única coleção com 2,5 K RU/s. Você não verá nenhum nível de taxa de transferência de tooyour de alteração.

Em cada um desses casos, após a migração da sua coleção, você será ser capaz de toocustomize o nível de taxa de transferência ou dimensioná-lo para cima e para baixo como usuários de tooyour de baixa latência acesso tooprovide necessários. nível de taxa de transferência de saudação toochange depois de sua coleção foi migrado, simplesmente abra sua conta de banco de dados do Cosmos no hello portal do Azure, clique em escala, escolha sua coleção e, em seguida, ajustar o nível de taxa de transferência de hello, conforme mostrado no hello captura de tela a seguir:

![Como tooscale a taxa de transferência em Olá portal do Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Como minha cobrança será alterado depois que estou coleções com uma partição única toohello migrados?

Supondo que você tem 10 coleções de S1, 1 GB de armazenamento para cada região de US East Olá, e você migrar esses 10 S1 coleções too10 coleções com uma partição em 400 RU/s (nível mínimo de saudação). Se você mantiver as coleções de partição única 10 Olá por um mês inteiro, o sua fatura será semelhante ao seguinte:

![Como S1 preços para 10 coleções comparam too10 coleções usando preços para uma coleção de partição única](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>E se eu precisar de mais de 10 GB de armazenamento?

Se você tem uma coleção com um nível de desempenho S1, S2 ou S3 ou tem uma coleção de partição única, que têm 10 GB de armazenamento disponível, você pode usar toomigrate de ferramenta de migração de dados de banco de dados do Cosmos Olá tooa seus dados particionados coleção com praticamente armazenamento ilimitado. Para obter informações sobre os benefícios de saudação de uma coleção particionada, consulte [particionamento e escala no banco de dados do Azure Cosmos](documentdb-partition-data.md). Para obter informações sobre como toomigrate seus S1, S2, S3 ou coleção de tooa particionado de partição única, consulte [migração de coleções de partição única toopartitioned](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>Alterar entre níveis de desempenho S1, S2 e S3 de saudação antes de 1 de agosto de 2017?

Somente as contas existentes com desempenho S1, S2 e S3 serão capaz de toochange e alter diferentes níveis de desempenho por meio do portal hello ou programaticamente. Por 1 de agosto de 2017, Olá S1, S2, e os níveis de desempenho S3 deixarão de ficar disponíveis. Se você alterar a coleção de partição única tooa S1, S3 ou S3, você não pode retornar toohello níveis de desempenho S1, S2 ou S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Como saberei quando minha coleção migrou?

migração de saudação ocorrerá em 31 de julho de 2017. Se você tiver uma coleção que usa Olá S1, S2 ou S3 níveis de desempenho, equipe de banco de dados do Cosmos Olá entrará em contato com você por email antes de migração de saudação ocorre. Depois que a migração de saudação é concluída em 1 de agosto de 2017, Olá portal do Azure mostrará que sua coleção usa os preços padrão.

![Como tooconfirm sua coleção foi migrado toohello faixa de preços padrão](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Como migrar do hello S1, S2, S3 desempenho níveis toosingle coleções com uma partição por conta própria?

Você pode migrar de saudação S1, S2, e níveis de desempenho de S3 toosingle coleções de partição usando Olá portal do Azure ou programaticamente. Você pode fazer isso em seu próprio antes de 1 de agosto toobenefit das opções de taxa de transferência flexível Olá disponíveis com coleções com uma única partição, ou vai migrar suas coleções para você em 31 de julho de 2017.

**toomigrate toosingle coleções com uma partição usando Olá portal do Azure**

1. Em Olá [ **portal do Azure**](https://portal.azure.com), clique em **o banco de dados do Azure Cosmos**, selecione Olá toomodify de conta de banco de dados do Cosmos. 
 
    Se **banco de dados do Azure Cosmos** não é Olá Jumpbar, clique em >, role muito**bancos de dados**, selecione **banco de dados do Azure Cosmos**e, em seguida, selecione a conta de documentos de saudação.  

2. No menu de recurso hello, em **contêineres**, clique em **escala**, selecione Olá coleção toomodify na lista suspensa de saudação e, em seguida, clique em **preço**. As contas que usam a taxa de transferência predefinida têm um tipo de preço de S1, S2 ou S3.  Em Olá **Escolher tipo de preços** folha, clique em **padrão** toochange definido toouser taxa de transferência e, em seguida, clique em **selecione** toosave sua alteração.

    ![Captura de tela da folha de configurações de saudação mostrando onde toochange Olá valor de taxa de transferência](./media/performance-levels/change-performance-set-thoughput.png)

3. Em Olá **escala** folha, Olá **preço** é alterada muito**padrão** e hello **(RU/s) de taxa de transferência** caixa é exibida com um valor padrão de 400. Taxa de transferência do conjunto Olá entre 400 e 10.000 [unidades de solicitação ](request-units.md) /segundo (RU/s). Olá **fatura mensal estimado** final Olá Olá page atualiza automaticamente tooprovide uma estimativa de custo mensal de saudação. 

    >[!IMPORTANT] 
    > Depois de salvar suas alterações e mover toohello faixa de preços padrão, você não poderá reverter toohello níveis de desempenho S1, S2 ou S3.

4. Clique em **salvar** toosave suas alterações.

    Se determinar que precisa de uma taxa de transferência maior (mais de 10.000 RU/s) ou mais armazenamento (mais de 10 GB), você poderá criar uma coleção particionada. toomigrate uma única partição tooa particionada coleção, consulte [migração de coleções de partição única toopartitioned](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > A alteração de S1, S2 ou S3 tooStandard pode levar too2 minutos.
    > 
    > 

**Olá de toomigrate toosingle coleções com uma partição usando o SDK do .NET**

Outra opção para alterar os níveis de desempenho de suas coleções é por meio de nossos SDKs. Esta seção aborda apenas alterar o desempenho da coleção nível usando nosso [API .NET do DocumentDB](documentdb-sdk-dotnet.md), mas o processo de saudação é semelhante para nossos outros SDKs.

Aqui está um trecho de código para alterar too5 de taxa de transferência de coleção hello, 000 unidades de solicitação por segundo:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Visite [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) exemplos adicionais de tooview e saber mais sobre os métodos de nossa oferta:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Como serei afetado se eu for um cliente EA?

Os clientes EA será protegido até o final de saudação do seu contrato.

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre preços e gerenciamento de dados com o banco de dados do Azure Cosmos, explore esses recursos:

1.  [Particionando dados no Cosmos DB](documentdb-partition-data.md). Compreenda a diferença de saudação entre o contêiner de partição única e contêineres particionados, bem como dicas sobre como implementar um tooscale de estratégia de particionamento perfeitamente.
2.  [Preços do Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Saiba mais sobre o custo de saudação de provisionamento de taxa de transferência e consumo de armazenamento.
3.  [Unidades de solicitação](request-units.md). Compreenda o consumo de saudação de taxa de transferência para tipos diferentes de operação, consultas de leitura, gravação, por exemplo.
