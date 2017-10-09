---
title: aaaSet pontos de extremidade em uma VM do Windows classic | Microsoft Docs
description: "Saiba tooset pontos de extremidade para uma VM do Windows no hello comunicação tooallow de portal clássico do Azure com uma máquina virtual do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Como tooset pontos de extremidade em uma máquina virtual do Windows clássica no Azure
Olá a todas as janelas de máquinas virtuais que você criar no Azure usando o modelo de implantação clássico Olá automaticamente podem se comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual. No entanto, os computadores Olá Internet ou outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual. Este artigo também está disponível para [máquinas virtuais Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Em Olá **Gerenciador de recursos de** modelo de implantação, pontos de extremidade são configurados usando **grupos de segurança de rede (NSGs)**. Para obter mais informações, consulte [permitir acesso externo tooyour VM usando Olá portal do Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Quando você cria uma máquina virtual Windows no hello portal do Azure, os pontos de extremidade comuns como as de área de trabalho remota e comunicação remota do Windows PowerShell são geralmente criados para você automaticamente. Você pode configurar pontos de extremidade adicionais durante a criação de máquina virtual de hello, ou posteriormente, conforme necessário.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Próximas etapas
* toouse um tooset de cmdlet do PowerShell do Azure a um ponto de extremidade VM, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse um toomanage de cmdlet do PowerShell do Azure uma ACL em um ponto de extremidade, consulte [listas de controle de acesso de gerenciamento (ACLs) para pontos de extremidade usando o PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Se você criou uma máquina virtual no modelo de implantação do Gerenciador de recursos de saudação, você pode usar Azure PowerShell muito[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfego toohello VM.
