---
title: "taxa de transferência aaaProvision para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooset provisionados taxa de transferência para seu banco de dados do Azure Cosmos containsers coleções, gráficos e tabelas."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Definir a produtividade de contêineres do Azure Cosmos DB

Você pode definir a taxa de transferência para os contêineres de banco de dados do Azure Cosmos Olá portal do Azure ou usando Olá SDKs de cliente. 

Olá a tabela a seguir lista a taxa de transferência Olá disponível para os contêineres:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Contêiner de partição única</strong></p></td>
            <td valign="top"><p><strong>Contêiner particionado</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Produtividade mínima</p></td>
            <td valign="top"><p>400 unidades de solicitação por segundo</p></td>
            <td valign="top"><p>2.500 unidades de solicitação por segundo</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Produtividade máxima</p></td>
            <td valign="top"><p>10.000 unidades de solicitação por segundo</p></td>
            <td valign="top"><p>Ilimitado</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>taxa de transferência tooset hello usando Olá portal do Azure

1. Em uma nova janela, abra Olá [portal do Azure](https://portal.azure.com).
2. Na barra de saudação à esquerda, clique em **o banco de dados do Azure Cosmos**, ou clique em **mais serviços** na parte inferior do hello, role muito**bancos de dados**e, em seguida, clique em **banco de dados do Azure Cosmos**.
3. Selecione sua conta do Cosmos DB.
4. Na nova janela de hello, clique em **Gerenciador de dados (visualização)** no menu de navegação hello.
5. Na nova janela de hello, expanda o banco de dados e o contêiner e, em seguida, clique em **configurações de escala &**.
6. Na nova janela de hello, digite o novo valor de taxa de transferência hello, em Olá **taxa de transferência** caixa e, em seguida, clique em **salvar**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>taxa de transferência tooset hello usando Olá API DocumentDB para .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Perguntas frequentes sobre taxa de transferência

**Posso configurar meu tooless de taxa de transferência de 400 RU/s?**

400 RU/s é Olá taxa de transferência mínima disponível em coleções de partição única de banco de dados do Cosmos (2500 RU/s é Olá mínimo para as coleções particionadas). Solicitação de unidades são definidas em intervalos de 100 RU/s, mas a taxa de transferência não é possível definir too100 RU/s ou qualquer valor menor do que 400 RU/s. Se você estiver procurando por um método econômico toodevelop e Cosmos banco de dados de teste, você pode usar o hello livre [emulador de banco de dados do Azure Cosmos](local-emulator.md), que pode ser implantado localmente, sem nenhum custo. 

**Como definir o througput usando Olá MongoDB API?**

Não há nenhuma taxa de transferência do MongoDB API extensão tooset. Olá recomendação é toouse hello API DocumentDB, conforme mostrado no [tooset taxa de transferência de saudação usando Olá API DocumentDB para .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o provisionamento e escala planeta contínuo com Cosmos DB, consulte [particionamento e o dimensionamento com o banco de dados do Cosmos](partition-data.md).
