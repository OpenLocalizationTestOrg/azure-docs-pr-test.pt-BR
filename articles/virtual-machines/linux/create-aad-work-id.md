---
title: aaaCreate uma identidade ou de estudante no AAD para Linux | Microsoft Docs
description: "Saiba como toocreate uma identidade ou de estudante no Active Directory do Azure toouse com máquinas virtuais Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a>Criando uma identidade de empresa ou escola no Active Directory do Azure toouse com VMs do Linux
Se você criou uma conta do Azure pessoal ou ter uma assinatura do MSDN pessoal e criado Olá conta do Azure tootake aproveitar créditos do Azure MSDN hello – você usou uma *conta da Microsoft* identidade toocreate-lo. Muitos recursos excelentes do Azure – [modelos de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) é um exemplo – requerem uma conta corporativa ou de Estudante (uma identidade gerenciada pelo Active Directory do Azure) toowork. Você pode seguir as instruções de saudação abaixo toocreate que um novo trabalho ou escola conta porque Felizmente, uma das melhores coisas Olá sobre sua conta do Azure pessoal é que ela vem com um domínio do Active Directory do Azure padrão que você pode usar toocreate um novo trabalho ou escola conta que você pode usar com os recursos do Azure que a exigem.

No entanto, alterações recentes torná-lo toomanage possíveis sua assinatura com qualquer tipo de conta do Azure usando Olá `azure login` método de logon interativo descrito [aqui](../../xplat-cli-connect.md). Você pode usar esse mecanismo, ou você pode seguir as instruções de saudação que seguem. Você também pode [criar uma identidade ou de estudante no Active Directory do Azure toouse com VMs do Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

