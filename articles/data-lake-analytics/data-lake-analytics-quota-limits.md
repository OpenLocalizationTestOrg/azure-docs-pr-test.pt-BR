---
title: "aaaAzure limites de cota de análise Data Lake | Microsoft Docs"
description: Saiba como tooadjust e aumentar a cota limita em contas do Azure Data Lake Analytics (ADLA).
services: data-lake-analytics
keywords: "Análise Azure Data Lake"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Limites de Cota do Azure Data Lake Analytics

Saiba como tooadjust e aumentar a cota limita em contas do Azure Data Lake Analytics (ADLA). Conhecer esses limites pode ajudar você a entender o comportamento do seu trabalho U-SQL. Todos os limites de cota são flexíveis, para que você pode aumentar os limites máximos Olá alcançar toous.

## <a name="azure-subscriptions-limits"></a>Limites das assinaturas do Azure

**Número máximo de contas do ADLA por assinatura:**5

 Este é o número de máximo de saudação de contas ADLA que pode ser criado por assinatura. Se você tentar conta ADLA toocreate um sexto, você obterá um erro "Você atingiu Olá o número máximo de contas da análise Data Lake permitidas (5) na região em nome de assinatura". Nesse caso, exclua todas as contas ADLA não utilizadas ou chegar toous por [abrindo um tíquete de suporte](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Limites da conta do ADLA

**Número máximo de AUs (Unidades de Análise) por conta:** 250

Este é o número de máximo de saudação de AUs que podem ser executados simultaneamente em sua conta. Se o total de AUs em execução em todos os trabalhos exceder esse limite, novos trabalhos serão colocados na fila automaticamente. Por exemplo:

* Se você tiver apenas um trabalho em execução com 250 Austrália, quando você enviar um segundo trabalho que irá esperar na fila de trabalhos Olá Olá primeiro trabalho é concluído.
* Se você já tiver cinco trabalhos em execução e cada um está usando 50 Austrália, quando você enviar um trabalho sexto que precisa de 20 Austrália aguardar na fila de trabalhos Olá até que haja 20 Austrália disponíveis.

**Número máximo de trabalhos U-SQL simultâneos por conta:**  20

Este é o número máximo de saudação de trabalhos que podem ser executados simultaneamente em sua conta. Exceder esse valor faz com que os trabalhos mais recentes sejam enfileirados automaticamente.

## <a name="adjust-adla-quota-limits-per-account"></a>Ajustar os limites de cota do ADLA por conta

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Escolha uma conta ADLA que você já criou.
3. Clique em **Propriedades**.
4. Ajustar **paralelismo** e **trabalhos simultâneos** toosuit suas necessidades.

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Aumente os limites máximos de cota

1. Abra uma solicitação de suporte no Portal do Azure.

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Selecione o tipo de problema Olá **cota**.
3. Selecione sua **Assinatura**(Verifique se ela não é uma assinatura de "teste").
4. Selecione o tipo de cota **Data Lake Analytics**.

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. Na folha de problema hello, explique o limite de aumento solicitado com **detalhes** de por que você precisa que essa capacidade extra.

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Verifique se suas informações de contato e criar solicitação de suporte de saudação.

A Microsoft analisa sua solicitação e tenta tooaccommodate necessidades de sua empresa assim que possível.

## <a name="next-steps"></a>Próximas etapas

* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Gerenciar a Análise Azure Data Lake usando o Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
