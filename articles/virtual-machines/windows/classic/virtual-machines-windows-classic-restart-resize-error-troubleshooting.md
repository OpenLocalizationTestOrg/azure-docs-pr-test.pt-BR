---
title: aaaVM reiniciar ou redimensionar problemas | Microsoft Docs
description: "Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure
> [!div class="op_single_selector"]
> * [Clássico](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Gerenciador de Recursos](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

Quando você tentar toostart uma parada Máquina Virtual (VM) do Azure, ou redimensiona uma VM do Azure existente, o erro comum de saudação que encontrar é uma falha de alocação. Esse erro ocorre quando o cluster hello ou região ou não tem recursos disponíveis ou não suporte Olá solicitada tamanho da VM.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Coletar logs de auditoria
toostart de solução de problemas, auditoria Olá coletar registra o erro de saudação de tooidentify associado Olá problema.

No portal do Azure de Olá, clique em **procurar** > **máquinas virtuais** > *sua máquina virtual do Windows*  >   **Configurações de** > **logs de auditoria**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: erro ao iniciar uma VM parada
Tente toostart uma VM parada mas obterão uma falha de alocação.

### <a name="cause"></a>Causa
solicitação de Olá Olá toostart interrompido VM tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem hello. No entanto, o cluster de saudação não tem solicitação de saudação do espaço livre disponível toofulfill.

### <a name="resolution"></a>Resolução
* Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região, mas não a um grupo de afinidades.
* Excluir Olá interrompido VM.
* Recrie Olá VM no novo serviço de nuvem hello usando discos de saudação.
* Iniciar Olá recriado VM.

Se você receber um erro ao tentar toocreate um novo serviço de nuvem, tente novamente mais tarde ou alterar a região Olá Olá serviço de nuvem.

> [!IMPORTANT]
> novo serviço de nuvem Olá terá um novo nome e o VIP, portanto, será necessário toochange essas informações para todas as dependências de saudação que usam essas informações para o serviço de nuvem existente hello.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: erro ao redimensionar uma VM existente
Tente tooresize uma VM existente mas obterão uma falha de alocação.

### <a name="cause"></a>Causa
solicitação Olá Olá tooresize VM tem toobe tentado no cluster original Olá serviço em nuvem Olá hosts. No entanto, não oferece suporte cluster Olá Olá solicitado tamanho da VM.

### <a name="resolution"></a>Resolução
Reduzir Olá solicitado tamanho da VM e repetição Olá redimensionar a solicitação.

* Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > *sua máquina virtual* > **Configurações** > **Tamanho**. Para obter etapas detalhadas, consulte [redimensionar a máquina virtual de saudação](https://msdn.microsoft.com/library/dn168976.aspx).

Se não for possível tooreduce Olá tamanho da VM, siga estas etapas:

* Criar um novo serviço de nuvem, garantir que não é vinculado tooan grupo de afinidade e não associado a uma rede virtual que é o grupo de afinidade tooan vinculado.
* Crie uma nova VM maior nele.

Você pode consolidar todas as suas VMs em Olá mesmo serviço de nuvem. Se seu serviço de nuvem existente estiver associado uma rede virtual com base em região, você pode conectar Olá nova nuvem serviço toohello rede virtual existente.

Se o serviço de nuvem existente Olá não está associado uma rede virtual com base em região, depois você ter toodelete Olá VMs no serviço de nuvem existente hello e recriá-los no novo serviço de nuvem Olá de seus discos. No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e o VIP, portanto, será necessário tooupdate para todas as dependências de saudação que atualmente usam essas informações para o serviço de nuvem existente hello.

## <a name="next-steps"></a>Próximas etapas
Se você encontrar problemas ao criar uma nova VM do Windows no Azure, veja [Solucionar problemas de implantação com a criação de uma máquina virtual do Windows no Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

