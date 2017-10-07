---
title: "aaaTroubleshoot clássico de implantação de VM do Linux | Microsoft Docs"
description: "Solucionar problemas de implantação clássica ao criar uma nova máquina virtual Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Solucionar problemas de implantação clássica ao criar uma nova máquina virtual Linux no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para a versão do Gerenciador de recursos de saudação deste artigo, consulte [aqui](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Coletar logs de auditoria
toostart de solução de problemas, auditoria Olá coletar registra o erro de saudação de tooidentify associado Olá problema.

No portal do Azure de Olá, clique em **procurar** > **máquinas virtuais** > *sua máquina virtual do Windows*  >   **Configurações de** > **logs de auditoria**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** se Olá SO for Linux generalizado e ele é carregado e/ou capturado com hello generalizado configuração, não haja erros. Da mesma forma, se Olá SO é especializada do Linux, e ele é carregado e/ou capturado com hello especializado configuração, e não haja erros.

**Erros de upload:**

**N<sup>1</sup>:** se Olá SO for Linux generalizado, e ele é carregado como especializado, obterá um erro de tempo limite de provisionamento porque Olá VM está preso em Olá estágio de provisionamento.

**N<sup>2</sup>:** se Olá SO especializado do Linux, e ele é carregado como generalizado, você obterá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password.

**Resolução:**

tooresolve ambos esses erros, carregar Olá VHD original, disponível no local, com Olá a mesma configuração que para Olá SO (generalizado/especializado). tooupload como generalizado, lembre-se de toorun-desprovisionar primeiro. Consulte [criar e carregar um disco rígido Virtual que Olá contém sistema operacional Linux](create-upload-vhd.md) para obter mais informações.

**Erros de captura:**

**N<sup>3</sup>:** se Olá SO for Linux generalizado, e ele é capturado como especializado, você obterá um erro de tempo limite de provisionamento porque Olá original VM não é utilizável que está marcado como generalizado.

**N<sup>4</sup>:** se Olá SO especializado do Linux, e eles são capturados como generalizado, você obterá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password. Além disso, Olá original VM não é utilizável porque ele está marcado como especializadas.

**Resolução:**

tooresolve ambos esses erros, excluir imagem atual de saudação do portal de saudação e [recapturá-lo da saudação VHDs atuais](capture-image.md) com Olá a mesma configuração que para hello (generalizado/especializado) de sistema operacional.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação
Esse erro ocorre em situações quando nova solicitação de VM Olá é enviada tooa cluster que não tenha a solicitação de saudação do tooaccommodate de espaço livre disponível, ou não aceitar o tamanho da VM hello está sendo solicitado. Não é possível toomix outra série de VMs em Olá mesmo serviço de nuvem. Assim, se você quiser toocreate uma nova VM do que seu serviço de nuvem pode dar suporte a um tamanho diferente, Olá computação solicitação falhará.

Dependendo de restrições de Olá Olá do serviço de nuvem que você usar toocreate Olá nova VM, você pode encontrar um erro causado por uma das duas situações.

**Causa 1:** Olá serviço em nuvem é fixado tooa determinado cluster, ou é o grupo de afinidade tooan vinculado e tooa fixos, portanto, o cluster específico por design. Para solicitações de novos recursos de computação no grupo de afinidade serão tentadas por Olá mesmo cluster que hospedam os recursos existentes de saudação. No entanto, hello mesmo cluster talvez não suporte Olá solicitado tamanho da VM ou tiver espaço suficiente disponível, resultando em um erro de alocação. Isso é verdadeiro se o hello novos recursos são criados por meio de um novo serviço de nuvem ou um serviço de nuvem existente.

**Resolução 1:**

* Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região.
* Crie uma nova VM no novo serviço de nuvem hello.
  Se você receber um erro ao tentar toocreate um novo serviço de nuvem, tente novamente mais tarde ou alterar a região Olá Olá serviço de nuvem.

> [!IMPORTANT]
> Se você estivesse tentando toocreate uma nova VM em um serviço de nuvem existente, mas não foi possível e tinha toocreate um novo serviço de nuvem para sua nova VM, você pode escolher tooconsolidate todas as suas VMs em Olá mesmo serviço de nuvem. Assim, toodo excluir Olá VMs no serviço de nuvem existente hello e recapturá-los de seus discos no novo serviço de nuvem hello. No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e o VIP, portanto, será necessário tooupdate para todas as dependências de saudação que atualmente usam essas informações para o serviço de nuvem existente hello.
> 
> 

**Causa 2:** serviço de nuvem hello está associado uma rede virtual que é vinculado tooan grupo de afinidade, sendo tooa fixados cluster específico de design. Todas as novas solicitações de recursos de computação no grupo de afinidade, portanto, são feitas tentativas em Olá mesmo cluster que hospedam os recursos existentes de saudação. No entanto, hello mesmo cluster talvez não suporte Olá solicitado tamanho da VM ou tiver espaço suficiente disponível, resultando em um erro de alocação. Isso é verdadeiro se o hello novos recursos são criados por meio de um novo serviço de nuvem ou um serviço de nuvem existente.

**Resolução 2:**

* Crie uma nova rede virtual regional.
* Criar hello nova VM na nova rede virtual de saudação.
* [Conecte-se a sua rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nova rede virtual. Saiba mais sobre as [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Como alternativa, você pode [migrar sua rede de virtual baseado em grupos de afinidade de rede virtual tooa regionais](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e, em seguida, criar hello nova VM.

## <a name="next-steps"></a>Próximas etapas
Se você encontrar problemas ao iniciar uma VM do Linux parada ou redimensionar uma VM do Linux existente no Azure, consulte [Solucionar problemas de implantação clássico ao reinicializar ou redimensionar uma máquina virtual Linux existente no Azure](restart-resize-error-troubleshooting.md).

