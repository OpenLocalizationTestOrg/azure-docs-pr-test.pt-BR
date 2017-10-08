---
title: "problemas de aaaDeployment para perguntas frequentes sobre serviços de nuvem do Azure Microsoft | Microsoft Docs"
description: "Este artigo lista Olá perguntas frequentes sobre a implantação de serviços de nuvem do Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de implantação para Serviços de Nuvem do Azure: perguntas frequentes

Este artigo inclui perguntas frequentes sobre problemas de implantação para [Serviços de Nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Por que implantar um toohello de serviço de nuvem, às vezes, o slot de preparo falha com um erro de alocação de recursos se já houver uma implantação existente no slot de produção de hello?
Se um serviço de nuvem tem uma implantação em nenhum slot, serviço de nuvem inteira Olá é cluster específico tooa fixados. Isso significa que se uma implantação já existe no slot de produção de hello, uma nova implantação de preparo só pode ser alocada no mesmo cluster como o slot de produção de hello de saudação.

Falhas de alocação de ocorrerem quando o cluster Olá onde se encontra o serviço de nuvem não tem suficiente físico toosatisfy de recursos de computação sua solicitação de implantação.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Por que escalar vertical ou horizontalmente uma implantação do serviço de nuvem às vezes resulta em falha de alocação?
Quando um serviço de nuvem é implantado, ele normalmente obtém cluster específico tooa fixados. Isso significa que o dimensionamento das/out uma nuvem existente serviço deve alocar novas instâncias em Olá mesmo cluster. Se cluster hello está se aproximando da capacidade ou Olá desejado VM/tipo de tamanho não está disponível, Olá solicitação pode falhar.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Por que implantar um serviço de nuvem em um grupo de afinidades às vezes resulta em falha de alocação?
Um novo serviço de nuvem vazio do tooan de implantação pode ser alocado pela malha hello em qualquer cluster nessa região, a menos que o serviço de nuvem Olá é fixado tooan grupo de afinidade. Implantações toohello mesmo grupo de afinidade será tentado no hello mesmo cluster. Se o cluster hello está se aproximando da capacidade, a solicitação de saudação pode falhar.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Por que alterar o tamanho da VM ou adicionando um nova VM tooan serviço de nuvem existente, às vezes, resulta em falha de alocação?
clusters de saudação em um datacenter podem ter configurações diferentes dos tipos de máquina (por exemplo, uma série, série Av2, série D, série Dv2, série G, série H, etc.). Mas nem todos os clusters de saudação teria necessariamente todos os tipos de saudação de VMs. Por exemplo, se você tentar tooadd uma série D serviço de nuvem do VM tooa que já esteja implantado em um cluster somente de série de um, você terá uma falha de alocação. Isso também ocorrerá se você tentar toochange VM SKU tamanhos (por exemplo, alternando de uma série de tooa D série A).

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

toocheck de tamanhos de saudação disponíveis em sua região, consulte [Microsoft Azure: produtos disponíveis por região](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Por que implantar uma nuvem de serviço falha em algum momento devidas toolimits/cotas/restrições em minha assinatura ou o serviço?
Implantação de um serviço de nuvem pode falhar se recursos Olá toobe necessário alocada excederem padrão hello ou cota máximo permitido para o serviço no nível de região/datacenter hello. Para obter mais informações, consulte [Limites de Serviços de Nuvem](../azure-subscription-service-limits.md#cloud-services-limits).

Você também pode controlar Olá atual/cota de uso para sua assinatura no portal de saudação: Portal do Azure = > assinaturas = > \<apropriado da assinatura > = > "+ cota de uso".

Informações relacionadas ao uso/consumo de recursos também podem ser recuperadas por meio de saudação APIs de cobrança do Azure. Confira [API de uso de recursos do Azure (versão prévia)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Como posso alterar o tamanho de saudação de um serviço de nuvem implantado VM sem reimplantação?
Você não pode alterar o tamanho da VM Olá de um serviço de nuvem implantado sem reimplantação. Olá tamanho da VM é criada em Olá CSDEF, que só pode ser atualizada com uma reimplantação.

Para obter mais informações, consulte [como um serviço de nuvem do tooupdate](cloud-services-update-azure-service.md).

 
