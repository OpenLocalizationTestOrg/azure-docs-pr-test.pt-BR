---
title: "aaaTroubleshoot Implantando problemas de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Solução de problemas de implantação de máquina virtual do Windows no modelo de implantação do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>Solução de problemas de implantação de máquina virtual do Windows no Azure

tootroubleshoot problemas de implantação de máquina virtual (VM) no Azure, examine Olá [principais problemas](#top-issues) de falhas e resoluções comuns.

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.

## <a name="top-issues"></a>Principais problemas
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

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

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>Como usar e implantar uma imagem do cliente Windows no Azure?

Você pode usar o Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento + teste, desde que você tenha uma assinatura apropriada do Visual Studio (anteriormente conhecido como MSDN). Isso [artigo](client-images.md) contornos Olá requisitos de qualificação para executar o cliente do Windows no Azure e usos de saudação imagens da Galeria do Azure.

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>Como implantar uma máquina virtual usando Olá benefício de usar híbrida (HUB)?

Há duas maneiras diferentes toodeploy Windows as máquinas virtuais com hello benefício de uso do Azure híbrido.

Para uma assinatura do Enterprise Agreement:

•   Implantar VMs com base em imagens específicas do Marketplace pré-configuradas com o Benefício de Uso Híbrido do Azure.

Para o Enterprise Agreement:

•   Carregar uma VM personalizada e implantar usando um modelo do Resource Manager ou do Azure PowerShell.

Para obter mais informações, consulte Olá recursos a seguir:

 - [Visão geral sobre o Benefício de Uso Híbrido do Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [Perguntas frequentes para download](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - [Benefício do Uso Híbrido do Azure para o Windows Server e o Windows Client](hybrid-use-benefit-licensing.md).

 - [Como usar Olá benefício de usar híbrido no Azure](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Como ativar o crédito mensal para o Visual Studio Enterprise (BizSpark)

tooactivate seu mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>Como tooadd desenvolvimento/teste Enterprise toomy EA (Enterprise Agreement) tooget acessar imagens do cliente tooWindow?

assinaturas de toocreate de capacidade de saudação com base na Olá desenvolvimento/teste Enterprise oferecem é proprietários de tooAccount restrito que receberam permissão toodo caso por um administrador de empresa. Olá proprietário da conta cria assinaturas via Olá Portal de conta do Azure e, em seguida, deverá adicionar os assinantes ativos do Visual Studio como administradores. Para que eles podem gerenciar e usar recursos de saudação necessários para desenvolvimento e teste. Para obter mais informações, consulte [Desenvolvimento/Teste Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>Meus drivers estão ausentes para minha VM série N do Windows

Drivers para VMs baseadas em Windows estão localizados [aqui](n-series-driver-setup.md).

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Não é possível localizar uma instância GPU em minha VM série N

tootake vantagem dos recursos GPU Olá de VMs série N do Azure executando o Windows Server 2016 ou Windows Server 2012 R2, você deve instalar os drivers gráficos NVIDIA em cada VM após a implantação. Também há informações de instalação de driver disponíveis para [VMs do Windows](n-series-driver-setup.md) e [VMs do Linux](../linux/n-series-driver-setup.md).

## <a name="are-client-images-supported-for-n-series"></a>Imagens do cliente têm suporte para a série N?

Atualmente, o Azure suporta apenas série N em VMs que executam sistemas operacionais Windows Server e Linux.

## <a name="is-n-series-vms-available-in-my-region"></a>As VMs da série N estão disponíveis na minha região?

Você pode verificar a disponibilidade de saudação do hello [produtos disponíveis pela tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>Quais imagens de cliente é possível usar e implantar no Azure e como tooI obtê-los?

Você pode usar o Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento + teste, desde que você tenha uma assinatura apropriada do Visual Studio (anteriormente conhecido como MSDN). 

- Imagens do Windows 10 estão disponíveis na Galeria do Azure Olá em [qualificados de desenvolvimento/teste oferece](client-images.md#eligible-offers). 
- Assinantes do Visual Studio em qualquer tipo de oferta também podem [adequadamente preparar e criar](prepare-for-upload-vhd-image.md) uma imagem do Windows 7, Windows 8 ou Windows 10 64 bits e, em seguida, [carregar tooAzure](upload-generalized-managed.md). use Olá permanece toodev/teste limitado por assinantes ativos do Visual Studio.

Isso [artigo](client-images.md) contornos Olá requisitos de qualificação para executar o cliente do Windows no Azure e o uso de saudação imagens da Galeria do Azure.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Não tenho toosee capaz de família de tamanho da VM que desejo ao redimensionar a minha VM.

Quando uma máquina virtual está em execução, é o servidor físico tooa implantado. servidores físicos de saudação em regiões do Azure são agrupados em clusters de hardware físico comum. Redimensionar uma VM que exige clusters de hardware Olá VM toobe movido toodifferent é diferente dependendo de qual modelo de implantação foi usado toodeploy Olá VM.

- As VMs implantadas no modelo de implantação clássico, implantação de serviço de nuvem Olá devem ser removidas e reimplantado tamanho do toochange Olá VMs tooa outra família de tamanho.

- VMs implantadas no modelo de implantação do Gerenciador de recursos, você deve interromper todas as VMs no conjunto antes de alterar o tamanho de saudação de qualquer máquina virtual no conjunto de disponibilidade de saudação de disponibilidade de saudação.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Olá listado tamanho da VM não é suportado durante a implantação no conjunto de disponibilidade.

Escolha um tamanho que é compatível com cluster do conjunto de disponibilidade hello. Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM achar que precisa e tem que ser seu toohello implantação primeiro que conjunto de disponibilidade.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>É possível adicionar um conjunto de disponibilidade de tooan clássico VM existente?

Sim. Você pode adicionar um existente clássico VM tooa nova ou conjunto de disponibilidade existente. Para obter mais informações, consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Próximas etapas
Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).

Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.
