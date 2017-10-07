---
title: "aaaTroubleshoot implantação de VM do Linux-RM | Microsoft Docs"
description: "Solucionar problemas de implantação do Resource Manager ao criar uma nova máquina virtual Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Solucionar problemas de implantação do Resource Manager com a criação de uma nova máquina virtual Linux no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Principais problemas
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Para outros problemas de implantação de VM e perguntas, confira [Solucionar problemas de implantação de máquina virtual Linux no Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Coletar logs de atividades
toostart solução de problemas, atividade de coletar Olá registra o erro de saudação de tooidentify associado Olá problema. Hello links a seguir contêm informações detalhadas sobre Olá processo toofollow.

[Exibir operações de implantação](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Exibir logs de atividade toomanage Azure recursos](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** se Olá SO for Linux generalizado e ele é carregado e/ou capturado com hello generalizado configuração, não haja erros. Da mesma forma, se Olá SO é especializada do Linux, e ele é carregado e/ou capturado com hello especializado configuração, e não haja erros.

**Erros de upload:**

**N<sup>1</sup>:** se Olá SO for Linux generalizado, e ele é carregado como especializado, obterá um erro de tempo limite de provisionamento porque Olá VM está preso em Olá estágio de provisionamento.

**N<sup>2</sup>:** se Olá SO especializado do Linux, e ele é carregado como generalizado, você obterá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password.

**Resolução:**

tooresolve ambos esses erros, carregar Olá VHD original, disponível no local, com Olá a mesma configuração que para Olá SO (generalizado/especializado). tooupload como generalizado, lembre-se de toorun-desprovisionar primeiro.

**Erros de captura:**

**N<sup>3</sup>:** se Olá SO for Linux generalizado, e ele é capturado como especializado, você obterá um erro de tempo limite de provisionamento porque Olá original VM não é utilizável que está marcado como generalizado.

**N<sup>4</sup>:** se Olá SO especializado do Linux, e eles são capturados como generalizado, você obterá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password. Além disso, Olá original VM não é utilizável porque ele está marcado como especializadas.

**Resolução:**

tooresolve ambos esses erros, excluir imagem atual de saudação do portal de saudação e [recapturá-lo da saudação VHDs atuais](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) com Olá a mesma configuração que para hello (generalizado/especializado) de sistema operacional.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação
Esse erro ocorre em situações quando Olá nova solicitação VM é cluster tooa fixo que não oferece suporte a tamanho da VM hello está sendo solicitado ou não tem uma solicitação de saudação do tooaccommodate de espaço livre disponível.

**Causa 1:** não oferece suporte a cluster Olá Olá solicitado tamanho da VM.

**Resolução 1:**

* Repita a solicitação de saudação com um tamanho menor de VM.
* Se hello tamanho Olá solicitado de que VM não pode ser alterada:
  * Pare todas as VMs Olá Olá conjunto de disponibilidade.
    Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.
  * Depois que todos hello parar máquinas virtuais, criar hello nova VM no hello desejado de tamanho.
  * Iniciar Olá nova VM primeiro e, em seguida, selecione Olá interrompido VMs e clique em **iniciar**.

**Causa 2:** Olá cluster não tem recursos gratuitos.

**Resolução 2:**

* Repita a solicitação de hello mais tarde.
* Se hello nova VM pode ser definida parte de uma disponibilidade diferente
  * Criar uma nova VM em um conjunto de disponibilidade diferente (em Olá mesma região).
  * Adicionar Olá nova VM toohello mesma rede virtual.

## <a name="next-steps"></a>Próximas etapas
Se você encontrar problemas ao iniciar uma VM do Linux parada ou redimensionar uma VM do Linux existente no Azure, consulte [Solucionar problemas de implantação do Resource Manager ao reinicializar ou redimensionar uma máquina virtual Linux existente no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

