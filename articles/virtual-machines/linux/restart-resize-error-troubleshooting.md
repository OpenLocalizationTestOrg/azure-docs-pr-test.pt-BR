---
title: aaaVM reiniciar ou redimensionar problemas no Azure | Microsoft Docs
description: "Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Solucionar problemas de implantação ao reiniciar ou redimensionar uma VM Linux existente no Azure
Quando você tentar toostart uma parada Máquina Virtual (VM) do Azure, ou redimensiona uma VM do Azure existente, o erro comum de saudação que encontrar é uma falha de alocação. Esse erro ocorre quando o cluster hello ou região ou não tem recursos disponíveis ou não suporte Olá solicitada tamanho da VM.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Coletar logs de atividades
toostart solução de problemas, atividade de coletar Olá registra o erro de saudação de tooidentify associado Olá problema. Olá links a seguir contêm informações detalhadas sobre o processo de saudação:

[Exibir operações de implantação](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Exibir logs de atividade toomanage Azure recursos](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: erro ao iniciar uma VM parada
Tente toostart uma VM parada mas obterão uma falha de alocação.

### <a name="cause"></a>Causa
solicitação de Olá Olá toostart interrompido VM tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem hello. No entanto, o cluster de saudação não tem solicitação de saudação do espaço livre disponível toofulfill.

### <a name="resolution"></a>Resolução
* Pare Olá todas as VMs em disponibilidade Olá definido e, em seguida, reiniciar cada máquina virtual.
  
  1. Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.
  2. Depois que todos os Olá parar de VMs, selecione cada uma das VMs Olá interrompido e clique em Iniciar.
* Repita a solicitação de reinicialização de hello mais tarde.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: erro ao redimensionar uma VM existente
Tente tooresize uma VM existente mas obterão uma falha de alocação.

### <a name="cause"></a>Causa
solicitação Olá Olá tooresize VM tem toobe tentado no cluster original Olá serviço em nuvem Olá hosts. No entanto, não oferece suporte cluster Olá Olá solicitado tamanho da VM.

### <a name="resolution"></a>Resolução
* Repita a solicitação de saudação com um tamanho menor de VM.
* Se hello tamanho Olá solicitado de que VM não pode ser alterada:
  
  1. Pare todas as VMs Olá Olá conjunto de disponibilidade.
     
     * Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.
  2. Depois que todos os hello VMs parar, redimensione a VM de saudação desejado tooa tamanho maior.
  3. Selecione Olá redimensionado VM e clique em **iniciar**, e, em seguida, iniciar Olá interrompido VMs.

## <a name="next-steps"></a>Próximas etapas
Se você encontrar problemas ao criar uma nova VM do Linux no Azure, veja [Solucionar problemas de implantação com a criação de uma nova máquina virtual do Linux no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

