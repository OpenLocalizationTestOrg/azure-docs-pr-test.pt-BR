---
title: "Problemas de implantação para perguntas frequentes sobre Serviços de Nuvem do Microsoft Azure | Microsoft Docs"
description: "Este artigo lista as perguntas frequentes sobre a implantação para Serviços de Nuvem do Microsoft Azure."
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
ms.openlocfilehash: cb62cd4c4635d9e837dff81a9c4543781dd11adb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de implantação para Serviços de Nuvem do Azure: perguntas frequentes

Este artigo inclui perguntas frequentes sobre problemas de implantação para [Serviços de Nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Você também pode consultar a [página de tamanho de VM de Serviços de Nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-to-the-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-the-production-slot"></a>Por que implantar um serviço de nuvem ao slot de preparo às vezes falha com um erro de alocação de recurso se já houver uma implantação existente no slot de produção?
Se um serviço de nuvem tiver uma implantação em cada slot, todo o serviço de nuvem será fixado a um cluster específico. Isso significa que, se uma implantação já existir no slot de produção, uma nova implantação de preparo só poderá ser alocada no mesmo cluster que o slot de produção.

Falhas de alocação de ocorrerem quando o cluster em que se encontra o serviço de nuvem não tem recursos físicos de computação suficientes para atender à sua solicitação de implantação.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Por que escalar vertical ou horizontalmente uma implantação do serviço de nuvem às vezes resulta em falha de alocação?
Quando um serviço de nuvem é implantado, ele geralmente é fixado a um cluster específico. Isso significa que escalar vertical/horizontalmente um serviço de nuvem existente deve alocar novas instâncias no mesmo cluster. Se o cluster estiver se aproximando da capacidade ou se o tamanho/tipo de VM desejado não estiver disponível, a solicitação poderá falhar.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Por que implantar um serviço de nuvem em um grupo de afinidades às vezes resulta em falha de alocação?
Uma nova implantação para um serviço de nuvem vazio pode ser alocada pela malha em qualquer cluster nessa região, a menos que o serviço de nuvem esteja fixado em um grupo de afinidades. As implantações no mesmo grupo de afinidade serão tentadas no mesmo cluster. Se o cluster estiver se aproximando da capacidade, a solicitação poderá falhar.

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-to-an-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Por que alterar o tamanho da VM ou adicionar uma nova VM a um serviço de nuvem existente às vezes resulta em falha de alocação?
Os clusters em um datacenter podem ter configurações diferentes de tipos de computador (por exemplo, série A, série Av2, série D, série Dv2, série G, série H etc.). Porém, nem todos os clusters necessariamente terão todos os tipos de VMs. Por exemplo, se você tentar adicionar uma VM da série D a um serviço de nuvem que já esteja implantado em um cluster somente da série A, ocorrerá uma falha de alocação. Isso também ocorrerá se você tentar alterar os tamanhos de SKU da VM (por exemplo, trocar da série A para a série D).

Para obter ajuda a reduzir essas falhas de alocação, consulte [Falha na alocação do Serviço de Nuvem: soluções](cloud-services-allocation-failures.md#solutions).

Para verificar os tamanhos disponíveis em sua região, consulte [Microsoft Azure: produtos disponíveis por região](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-to-limitsquotasconstraints-on-my-subscription-or-service"></a>Por que implantar um serviço de nuvem às vezes falha devido a limites/cotas/restrições em minha assinatura ou o serviço?
A implantação de um serviço de nuvem poderá falhar se os recursos que precisam ser alocados excederem a cota padrão ou máxima permitida para o serviço no nível da região/do datacenter. Para obter mais informações, consulte [Limites de Serviços de Nuvem](../azure-subscription-service-limits.md#cloud-services-limits).

Você também pode controlar a cota/uso atual para sua assinatura no portal: Portal do Azure => Assinaturas => \<assinatura adequada> => "Uso + cota".

Informações relacionadas ao uso/consumo de recursos também podem ser recuperadas por meio das APIs de Cobrança do Azure. Confira [API de uso de recursos do Azure (versão prévia)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-the-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Como posso alterar o tamanho de uma VM de serviço de nuvem implantada sem reimplantá-la?
Você não pode alterar o tamanho de uma VM de serviço de nuvem implantada sem reimplantá-la. O tamanho da VM é criado em CSDEF, que somente pode ser atualizado com uma reimplantação.

Para obter mais informações, consulte [Como atualizar um serviço de nuvem](cloud-services-update-azure-service.md).

 
