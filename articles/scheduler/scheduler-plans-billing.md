---
title: "aaaPlans e cobrança no Agendador do Azure"
description: "Planos e Cobrança no Agendador do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Planos e Cobrança no Agendador do Azure
## <a name="job-collection-plans"></a>Planos de Coleção de Trabalho
Coleções de trabalho são a entidade cobráveis Olá no Agendador do Azure. As coleções de trabalho contém vários trabalhos e vêm em três planos: Gratuito, Standard e Premium, que são descritos abaixo.

| **Plano de Coleção de Trabalho** | **Número máximo de trabalhos por Coleção de Trabalhos** | **Recorrência Máxima** | **Máximo de Coleções de Trabalho por Assinatura** | **Limites** |
|:--- |:--- |:--- |:--- |:--- |
| **Gratuito** |5 trabalhos por coleção de trabalhos |Uma vez por hora. Não é possível executar trabalhos com uma frequência maior do que uma vez por hora |Uma assinatura é permitida a coleção de trabalhos livre too1 |Não é possível usar [objeto de saída de autorização HTTP](scheduler-outbound-authentication.md) |
| **Standard** |50 trabalhos por coleção de trabalhos |Uma vez por minuto. Não é possível executar trabalhos com uma frequência maior do que uma vez por minuto |Uma assinatura é permitida a coleções de trabalhos padrão too100 |Conjunto de recursos de toofull de acesso do Agendador |
| **P10 Premium** |50 trabalhos por coleção de trabalhos |Uma vez por minuto. Não é possível executar trabalhos com uma frequência maior do que uma vez por minuto |Uma assinatura é permitida a too10, coleções de trabalho Premium de P10 000. <a href="mailto:wapteams@microsoft.com">Entre em contato conosco</a>para obter mais informações. |Conjunto de recursos de toofull de acesso do Agendador |
| **P20 Premium** |1000 trabalhos por coleção de trabalhos |Uma vez por minuto. Não é possível executar trabalhos com uma frequência maior do que uma vez por minuto |Uma assinatura é permitida a too10, coleções de trabalho Premium de P20 000. <a href="mailto:wapteams@microsoft.com">Entre em contato conosco</a>para obter mais informações. |Conjunto de recursos de toofull de acesso do Agendador |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Atualizações e Downgrades de Planos de Coleção de Trabalhos
Você pode atualizar ou fazer downgrade de um plano de coleção de trabalho a qualquer momento entre os planos de gratuita, Standard e Premium Olá. No entanto, ao fazer o downgrade de coleção de trabalhos livre tooa, downgrade Olá pode falhar para um Olá motivos a seguir:

* Uma coleção de trabalhos livre já existe na assinatura de saudação
* Um trabalho na coleção de trabalhos de saudação tem uma recorrência maior que o permitido para trabalhos em coleções de trabalhos livre. recorrência máxima de saudação permitida em uma coleção de trabalhos livre é uma vez por hora
* Há mais de 5 trabalhos na coleção de trabalhos de saudação
* Um trabalho na coleção de trabalhos de saudação tem uma ação HTTP ou HTTPS que usa um [objeto de saída de autorização HTTP](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Planos de cobrança e do Azure
As assinaturas não são cobradas para coleções de trabalhos gratuitas. Se você tiver mais de 100 coleções de trabalho padrão (10 cobrança unidades padrão), é um toohave lidam melhor todas as coleções de trabalhos no plano de premium Olá.

Se você tiver uma coleção de trabalhos standard e uma coleção de trabalhos premium, será cobrada uma unidade de cobrança standard *e* uma unidade de cobrança premium. contas de serviço do Agendador Olá com base no número de saudação de coleções de trabalho ativo que são definidas tooeither standard ou premium; Isso é explicado mais próximas duas seções de saudação.

## <a name="standard-billable-units"></a>Unidades faturáveis Standard
Uma unidade faturável padrão pode incluir o too10 coleções de trabalhos padrão. Como uma coleção de trabalhos padrão pode ter os trabalhos de too50 por coleção de trabalhos, uma unidade de cobrança padrão permite que um toohave de assinatura, os trabalhos de too500 – backup tooalmost milhões de 22 execuções de trabalho por mês.

Se você tiver entre 1 e 10 coleções de trabalhos standard, você será cobrado por 1 unidade de cobrança standard. Se você tiver entre 11 e 20 coleções de trabalhos standard, você será cobrado por 2 unidades de cobrança standard. Se você tiver entre 21 e 30 coleções de trabalhos standard, você será cobrado por 3 unidades de cobrança standard e assim por diante.

## <a name="p10-premium-billable-units"></a>Unidades faturáveis Premium P10
Uma unidade de faturável premium P10 pode incluir o too10, 000 coleções de trabalho premium de P10. Como uma coleção de trabalho premium P10 pode ter trabalhos too50 por coleção de trabalhos, uma unidade de cobrança premium permite que um toohave assinatura backup too500, 000 trabalhos – backup tooalmost bilhões de 22 execuções de trabalho por mês.

Se você tiver entre 1 e 10.000 coleções de trabalhos premium P10, você será cobrado por 1 unidade de cobrança premium. Se você tiver entre 10.001 e 20.000 coleções de trabalhos premium, você será cobrado por 2 unidades de cobrança premium P10 e assim por diante.

Assim, o trabalho premium de P10 coleções têm Olá mesma funcionalidade como coleções de trabalhos padrão Olá mas fornecem uma quebra de preço caso seu aplicativo exigir muita coleções de trabalho.

## <a name="p20-premium-billable-units"></a>Unidades Faturáveis Premium P20
Uma unidade de faturável premium P20 pode incluir o too5, 000 P20 as coleções de trabalho premium. Como uma coleção de trabalhos P20 premium pode ter até too1, 000 trabalhos por coleção de trabalho, uma unidade de cobrança premium permite toohave uma assinatura para cima too5 000, 000 trabalhos – backup tooalmost bilhões de 220 execuções de trabalho por mês.

Coleções de trabalho P20 premium fornece Olá mesmas capacidades de coleções de trabalho P10 premium, mas também dá suporte a uma maior trabalhos número por coleção de trabalhos e o maior número total de trabalhos gerais que P10 premium permitindo que você toohave mais escalabilidade.

## <a name="billing-and-active-status"></a>Status de Cobrança e Ativo
Coleções de trabalho são sempre ativas, a menos que a assinatura inteira entrou em algum estado temporário desabilitado devido a problemas de toobilling. Olá apenas tooensure de forma que uma coleção de trabalho não será cobrada é tooeither defini-lo toohello *livre* coleção de trabalhos de plano ou toodelete hello.

Você pode desativar todos os trabalhos em uma coleção de trabalho em uma única operação, ele não altera o status de cobrança de saudação da coleção de trabalho hello – será de coleção de trabalhos de saudação *ainda* cobrado. Da mesma forma, coleções de trabalhos vazias são consideradas ativas e serão cobradas.

## <a name="pricing"></a>Preços
Para obter detalhes sobre preços, confira [Preços do Agendador](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Agendador do Azure](scheduler-concepts-terms.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador do Azure](scheduler-high-availability-reliability.md)

 [Limites, padrões e códigos de erro do Agendador do Azure](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

