---
title: "aaaTroubleshoot Implantando problemas de máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Solução de problemas de implantação de máquina virtual do Linux no modelo de implantação do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Solução de problemas de implantação de máquina virtual do Linux no Azure

tootroubleshoot problemas de implantação de máquina virtual (VM) no Azure, examine Olá [principais problemas](#top-issues) de falhas e resoluções comuns.

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.

## <a name="top-issues"></a>Principais problemas
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>não oferece suporte a cluster Olá Olá solicitado tamanho da VM
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Repita a solicitação de saudação com um tamanho menor de VM.
- Se hello tamanho Olá solicitado de que VM não pode ser alterada:
    - Pare todas as VMs Olá Olá conjunto de disponibilidade. Clique em **Grupos de recursos** > seu grupo de recursos > **Recursos** > seu conjunto de disponibilidade > **Máquinas Virtuais** > sua máquina virtual > **Parar**.
    - Depois que todos os Olá parar máquinas virtuais, criar hello VM de tamanho de saudação desejado.
    - Iniciar Olá nova VM primeiro e, em seguida, selecione Olá parado VMs e clique em Iniciar.


## <a name="hello-cluster-does-not-have-free-resources"></a>Olá cluster não tem recursos gratuitos
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Repetir a solicitação de hello mais tarde.
- Se hello nova VM pode ser definida parte de uma disponibilidade diferente
    - Criar uma máquina virtual em um conjunto de disponibilidade diferente (em Olá mesma região).
    - Adicionar Olá nova VM toohello mesma rede virtual.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Como ativar o crédito mensal para o Visual Studio Enterprise (BizSpark)

tooactivate seu mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Por que pode não instalar Olá GPU driver para uma VM do Ubuntu NV?

No momento, o suporte ao GPU do Linux está disponível apenas em VMs NC do Azure que executam o Ubuntu Server 16.04 LTS. Para saber mais, confira [Configurar drivers GPU para VMs série N executando o Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Meus drivers estão ausentes para minha VM série N do Linux

Drivers para VMs baseadas em Linux estão localizados [aqui](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Não é possível localizar uma instância GPU em minha VM série N

tootake vantagem dos recursos GPU Olá de VMs série N do Azure executando o Windows Server 2016 ou Windows Server 2012 R2, você deve instalar os drivers gráficos NVIDIA em cada VM após a implantação. Também há informações de instalação de driver disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md) e [VMs do Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>As VMs da série N estão disponíveis na minha região?

Você pode verificar a disponibilidade de saudação do hello [produtos disponíveis pela tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Não tenho toosee capaz de família de tamanho da VM que desejo ao redimensionar a minha VM.

Quando uma máquina virtual está em execução, é o servidor físico tooa implantado. servidores físicos de saudação em regiões do Azure são agrupados em clusters de hardware físico comum. Redimensionar uma VM que exige clusters de hardware Olá VM toobe movido toodifferent é diferente dependendo de qual modelo de implantação foi usado toodeploy Olá VM.

- As VMs implantadas no modelo de implantação clássico, implantação de serviço de nuvem Olá devem ser removidas e reimplantado tamanho do toochange Olá VMs tooa outra família de tamanho.

- VMs implantadas no modelo de implantação do Gerenciador de recursos, você deve interromper todas as VMs no conjunto antes de alterar o tamanho de saudação de qualquer máquina virtual no conjunto de disponibilidade de saudação de disponibilidade de saudação.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Olá listado tamanho da VM não é suportado durante a implantação no conjunto de disponibilidade.

Escolha um tamanho que é compatível com cluster do conjunto de disponibilidade hello. Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM achar que precisa e tem que ser seu toohello implantação primeiro que conjunto de disponibilidade.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Quais versões/distribuições do Linux têm suporte no Azure?

Você pode encontrar a lista de saudação em Linux em [Azure-Endorsed distribuições](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>É possível adicionar um conjunto de disponibilidade de tooan clássico VM existente?

Sim. Você pode adicionar um existente clássico VM tooa nova ou conjunto de disponibilidade existente. Para obter mais informações, consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Próximas etapas
Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).

Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.
