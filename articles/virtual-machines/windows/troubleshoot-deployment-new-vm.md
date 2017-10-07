---
title: "aaaTroubleshoot implantação de VM do Windows no Azure | Microsoft Docs"
description: "Solucionar problemas de implantação do Resource Manager ao criar uma nova máquina virtual Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Solucionar problemas de implantação ao criar uma nova VM Windows no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Principais problemas
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Para outros problemas de implantação de VM e perguntas, confira [Solucionar problemas de implantação de máquina virtual Windows no Azure](troubleshoot-deploy-vm.md).

## <a name="collect-activity-logs"></a>Coletar logs de atividades
toostart solução de problemas, atividade de coletar Olá registra o erro de saudação de tooidentify associado Olá problema. Hello links a seguir contêm informações detalhadas sobre Olá processo toofollow.

[Exibir operações de implantação](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Exibir logs de atividade toomanage Azure recursos](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** se Olá sistema operacional for Windows generalizado e ele é carregado e/ou capturado com hello generalizado configuração, não haja erros. Da mesma forma, se Olá SO é especializada do Windows, e ele é carregado e/ou capturado com hello especializado configuração, e não haja erros.

**Erros de upload:**

**N<sup>1</sup>:** se Olá sistema operacional for Windows generalizado e ele é carregado como especializado, você obterá um erro de tempo limite de provisionamento com hello VM presa na tela OOBE hello.

**N<sup>2</sup>:** se Olá SO é especializada do Windows, e ele é carregado como generalizado, você receberá um erro de falha de provisionamento com hello VM presa na tela OOBE Olá porque hello nova máquina virtual está em execução com o computador original Olá nome, nome de usuário e senha.

**Resolução**

tooresolve ambos esses erros, use [tooupload AzureRmVhd adicionar Olá VHD original](https://msdn.microsoft.com/library/mt603554.aspx), disponíveis no local, com hello configuração mesmo que para hello (generalizado/especializado) de sistema operacional. tooupload como generalizado, lembre-se sysprep toorun primeiro.

**Erros de captura:**

**N<sup>3</sup>:** se Olá sistema operacional for Windows generalizada e ele é capturado como especializado, você obterá um erro de tempo limite de provisionamento porque Olá original VM não é utilizável que está marcado como generalizado.

**N<sup>4</sup>:** se Olá SO é especializada do Windows, e eles são capturados como generalizado, você receberá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password. Além disso, Olá original VM não é utilizável porque ele está marcado como especializadas.

**Resolução**

tooresolve ambos esses erros, excluir imagem atual de saudação do portal de saudação e [recapturá-lo da saudação VHDs atuais](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) com Olá a mesma configuração que para hello (generalizado/especializado) de sistema operacional.

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação
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
Se você encontrar problemas ao iniciar uma VM do Windows parada ou redimensionar uma VM do Windows existente no Azure, consulte [Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Windows no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

