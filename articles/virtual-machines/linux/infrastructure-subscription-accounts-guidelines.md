---
title: aaaSubscription e conta para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para assinaturas e contas no Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Diretrizes de contas e assinaturas do Azure para VMs Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo se concentra em entender como o gerenciamento de conta e assinatura tooapproach como seu ambiente e a base de usuários aumenta.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Diretrizes de implementação para contas e assinaturas
Decisões:

* O conjunto de assinaturas e contas você precisa toohost a infra-estrutura ou carga de trabalho TI?
* Como toobreak para baixo Olá hierarquia toofit sua organização?

Tarefas:

* Definir sua hierarquia de organização lógica como você gostaria de toomanage-lo de um nível de assinatura.
* toomatch essa hierarquia lógica, definir contas Olá necessárias e assinaturas em cada conta.
* Crie conjunto de saudação de assinaturas e contas usando a convenção de nomenclatura.

## <a name="subscriptions-and-accounts"></a>Assinaturas e contas
toowork com o Azure, você precisa de uma ou mais assinaturas do Azure. Recursos como VMs (máquinas virtuais) ou redes virtuais existem em todas essas assinaturas.

* Os clientes corporativos normalmente têm um registro Enterprise, que é Olá recurso de mais alto na hierarquia de saudação e é tooone associado ou mais contas.
* Para clientes sem um registro da empresa e os consumidores, recursos de mais alto de saudação é conta hello.
* As assinaturas são tooaccounts associado, e pode haver uma ou mais assinaturas por conta. Informações no nível de assinatura de saudação de cobrança de registros do Azure.

Devido toohello limite de níveis de hierarquia de duas na relação de conta/assinatura Olá, é importante tooalign Olá convenção de nomeação toohello contas e assinaturas, cobrança necessidades. Por exemplo, se uma empresa global usa o Azure, eles podem escolher toohave uma conta por região e tem assinaturas gerenciadas no nível de região de hello:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Por exemplo, você pode usar o hello estrutura a seguir:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Se uma região decide toohave mais de um grupo específico de tooa associado de uma assinatura, convenção de nomenclatura Olá deve incorporar uma maneira tooencode Olá dados extras na conta hello ou nome de assinatura de saudação. Essa organização permite manipulando cobrança dados toogenerate Olá novos níveis de hierarquia durante a cobrança de relatórios:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

organização de saudação poderia ser semelhante a saudação de exemplo a seguir:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Fornecemos cobrança detalhada por meio de um arquivo para download, para uma única conta ou para todas as contas em um contrato empresarial.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

