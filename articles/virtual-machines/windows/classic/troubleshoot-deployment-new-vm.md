---
title: "Solucionar problemas de implantação clássica de VM do Windows | Microsoft Docs"
description: "Solucionar problemas de implantação clássica ao criar uma nova máquina virtual Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: troubleshooting
ms.date: 11/03/2016
ms.author: cjiang
ms.openlocfilehash: 5a1ad33bd8c287910458d26a96858e85c689fb16
ms.sourcegitcommit: adf6a4c89364394931c1d29e4057a50799c90fc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Solucionar problemas de implantação clássica ao criar uma nova máquina virtual Windows no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda o uso do modelo de implantação Clássica. A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos. Para a versão do Resource Manager deste artigo, clique [aqui](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Coletar logs de auditoria
Para iniciar a solução de problemas, colete os logs de auditoria para identificar o erro associado ao problema.

No Portal do Azure, clique em **Procurar** > **Máquinas virtuais** > *sua máquina virtual Windows* > **Configurações** > **Logs de auditoria**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** se o sistema operacional for Windows generalizado e ele for carregado e/ou capturado com a configuração generalizada, não haverá erros. Da mesma forma, se o sistema operacional for Windows especializado e ele for carregado e/ou capturado com a configuração especializada, não haverá erros.

**Erros de upload:**

**N<sup>1</sup>:** se o sistema operacional for Windows generalizado e ele for carregado como especializado, você receberá um erro de tempo limite de provisionamento, com a VM paralisada na tela do OOBE.

**N<sup>2</sup>:** se o sistema operacional for Windows especializado e ele for carregado como generalizado, você receberá um erro de falha no provisionamento com a VM paralisada na tela do OOBE, pois a nova VM estará em execução com o nome do computador, nome de usuário e senha originais.

**Resolução:**

Para resolver ambos os erros, carregue o VHD original, disponível no local, com a mesma configuração usada para o sistema operacional (generalizado/especializado). Para carregar como generalizado, lembre-se de executar sysprep primeiro. Veja [Criar e carregar um VHD do Windows Server no Azure](createupload-vhd.md) para obter mais informações.

**Erros de captura:**

**N<sup>3</sup>:** se o sistema operacional for Windows generalizado e ele for capturado como especializado, você receberá um erro de tempo limite de provisionamento, pois a VM original não será utilizável, já que estará marcada como generalizada.

**N<sup>4</sup>:** se o sistema operacional for Windows especializado e ele for capturado como generalizado, você receberá um erro de falha no provisionamento, pois a nova VM estará em execução com o nome do computador, nome de usuário e senha originais. Além disso, a VM original não será utilizável, já que estará marcada como especializada.

**Resolução:**

Para resolver ambos os erros, exclua a imagem atual do portal e [recapture-a dos VHDs atuais](capture-image.md) com a mesma configuração usada para o sistema operacional (generalizado/especializado).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação
Esse erro ocorre em situações nas quais a nova solicitação de VM é enviada para um cluster que não tem espaço livre disponível para acomodar a solicitação ou que não dá suporte ao tamanho de VM solicitado. Não é possível combinar séries diferentes de VMs no mesmo serviço de nuvem. Portanto, se você desejar criar uma nova VM de um tamanho diferente do qual o serviço de nuvem pode dar suporte, a solicitação de computação falhará.

Dependendo das restrições do serviço de nuvem usado para criar a nova VM, você poderá encontrar um erro causado por uma das duas situações.

**Causa 1:** o serviço de nuvem está fixo em um cluster específico ou está vinculado a um grupo de afinidades e, portanto, fixo em um cluster específico por design. Assim, há uma tentativa de fazer novas solicitações de recursos de computação nesse grupo de afinidades no mesmo cluster que hospeda os recursos existentes. No entanto, o mesmo cluster pode não dar suporte ao tamanho de VM solicitado ou pode não ter espaço suficiente disponível, resultando em um erro de alocação. Isso ocorre se os novos recursos forem criados por meio de um novo serviço de nuvem ou um serviço de nuvem existente.

**Resolução 1:**

* Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região.
* Crie uma nova VM no novo serviço de nuvem.
  Se você receber um erro ao tentar criar um novo serviço de nuvem, tente novamente mais tarde ou altere a região do serviço de nuvem.

> [!IMPORTANT]
> Se você estava tentando criar uma nova VM em um serviço de nuvem existente, mas não conseguiu e precisou criar um novo serviço de nuvem para sua nova VM, é possível optar por consolidar todas as VMs no mesmo serviço de nuvem. Para fazer isso, exclua as VMs do serviço de nuvem existente e as recapture por meio de seus discos no novo serviço de nuvem. No entanto, é importante lembrar-se de que o novo serviço de nuvem terá um novo nome e VIP e, portanto, será necessário atualizá-los em todas as dependências que atualmente usam essas informações para o serviço de nuvem existente.
> 
> 

**Causa 2:** o serviço de nuvem está associado a uma rede virtual vinculada a um grupo de afinidades e, portanto, está fixa em um cluster específico por design. Assim, há uma tentativa de fazer todas as novas solicitações de recursos de computação desse grupo de afinidades no mesmo cluster que hospeda os recursos existentes. No entanto, o mesmo cluster pode não dar suporte ao tamanho de VM solicitado ou pode não ter espaço suficiente disponível, resultando em um erro de alocação. Isso ocorre se os novos recursos forem criados por meio de um novo serviço de nuvem ou um serviço de nuvem existente.

**Resolução 2:**

* Crie uma nova rede virtual regional.
* Crie a nova VM na nova rede virtual.
* [Conecte sua rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) à nova rede virtual. Saiba mais sobre as [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Como alternativa, é possível [migrar a rede virtual baseada em grupo de afinidades para uma rede virtual regional](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e, em seguida, criar a nova VM.

## <a name="next-steps"></a>Próximas etapas
Se você encontrar problemas ao iniciar uma VM do Windows parada ou redimensionar uma VM do Windows existente no Azure, consulte [Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).

