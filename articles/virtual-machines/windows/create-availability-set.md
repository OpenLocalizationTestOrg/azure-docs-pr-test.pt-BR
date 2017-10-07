---
title: Definir aaaCreate uma disponibilidade VM no Azure | Microsoft Docs
description: "Saiba como definir toocreate uma disponibilidade gerenciada ou não gerenciado de disponibilidade definida para suas máquinas virtuais usando o Azure PowerShell ou Olá portal no modelo de implantação do Gerenciador de recursos de saudação."
keywords: conjunto de disponibilidade
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Aumentar a disponibilidade da VM criando um conjunto de disponibilidade do Azure 
Conjuntos de disponibilidade fornecem aplicativos de tooyour de redundância. Recomendamos o agrupamento de uma ou mais máquinas virtuais em um conjunto de disponibilidade. Essa configuração garante que durante a um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual será Olá disponível e atender 99,95% do SLA do Azure. Para obter mais informações, consulte Olá [SLA para máquinas virtuais](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Máquinas virtuais devem ser criados no hello mesmo grupo de recursos como conjunto de disponibilidade de saudação.
> 

Se você quiser que sua parte de toobe VM de um conjunto de disponibilidade, você precisa de disponibilidade de saudação do toocreate definir primeiro ou enquanto você estiver criando sua primeira VM no conjunto de saudação. Se a VM estiver usando discos gerenciados, o conjunto de disponibilidade de saudação deve ser criado como um conjunto de disponibilidade gerenciada.

Para obter mais informações sobre como criar e usar conjuntos de disponibilidade, consulte [gerenciar Olá disponibilidade das máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Use Olá portal toocreate um conjunto antes de criar suas VMs de disponibilidade
1. No menu de hub hello, clique em **procurar** e selecione **conjuntos de disponibilidade**.
2. Em Olá **folha de conjuntos de disponibilidade**, clique em **adicionar**.
   
    ![Captura de tela que mostra Olá adicionar botão para criar um novo conjunto de disponibilidade.](./media/create-availability-set/add-availability-set.png)
3. Em Olá **criar conjunto de disponibilidade** folha, informações de saudação completa para o conjunto.
   
    ![Captura de tela que mostra Olá informações que você precisa tooenter toocreate Olá disponibilidade definida.](./media/create-availability-set/create-availability-set.png)
   
   * **Nome** -nome hello deve ser 1-80 caracteres compostas de números, letras, pontos, sublinhados e traços. Olá primeiro caractere deve ser uma letra ou número. último caractere do Hello deve ser uma letra, número ou sublinhado.
   * **Domínios de falha** -domínios de falha definem o grupo de saudação de máquinas virtuais que compartilham um comutador de origem e de rede de alimentação comum. Por padrão, Olá VMs estiverem separadas em domínios de falha de toothree e podem ser alterado toobetween 1 e 3.
   * **Atualizar domínios** - cinco domínios de atualização são atribuídos por padrão, e isso pode ser definido toobetween 1 e 20. Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente. Por exemplo, se especificamos atualização cinco domínios, quando mais de cinco máquinas virtuais são configuradas em um único conjunto de disponibilidade, máquina virtual da sexta hello serão colocados no hello mesmo domínio de atualização como máquina virtual da primeira hello, hello sétima em Olá mesmo UD como máquina virtual da segunda Olá e assim por diante. ordem de saudação de reinicializações de saudação não pode ser sequencial, mas somente uma atualização de domínio será reinicializado por vez.
   * **Assinatura** -selecione Olá toouse de assinatura, se você tiver mais de um.
   * **Grupo de recursos** -selecione um grupo de recursos existente clicando em seta hello e selecionando um grupo de recursos de saudação lista suspensa. Você também pode criar um novo grupo de recursos digitando um nome. Olá nome pode conter nenhum dos seguintes caracteres de saudação: letras, números, pontos, traços, sublinhados e abertura ou parêntese de fechamento. Olá nome não pode terminar em um período. Todas Olá VMs no grupo de disponibilidade Olá precisam toobe criado no hello mesmo grupo de recursos Olá conjunto de disponibilidade.
   * **Local** -selecione um local na lista suspensa hello.
   * **Gerenciado** - selecione *Sim* toocreate uma disponibilidade gerenciada definida toouse com máquinas virtuais que usam discos gerenciados para o armazenamento. Selecione **não** se Olá VMs no conjunto de saudação usa discos de não gerenciados em uma conta de armazenamento.
   
4. Quando você terminar de inserir informações de saudação, clique em **criar**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Use Olá toocreate portal uma máquina virtual e uma disponibilidade definidos no hello mesmo tempo
Se você estiver criando uma nova VM usando o portal de saudação, você também pode criar uma novo conjunto de disponibilidade para Olá VM enquanto você cria Olá primeira VM no conjunto de saudação. Se você escolher toouse gerenciados discos para sua VM, será criado um conjunto de disponibilidade gerenciada.

![Captura de tela que mostra o processo de Olá para criar uma nova disponibilidade definida durante a criação de saudação VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Adicionar uma nova VM tooan existente conjunto de disponibilidade no portal de saudação
Para cada VM adicional que você criar que deve pertencer no conjunto de saudação, certifique-se de que você a crie em Olá mesmo **grupo de recursos** e, em seguida, selecione Olá disponibilidade existente, definida na etapa 3. 

![Captura de tela mostrando como tooselect um grupo de disponibilidade configurado toouse para sua VM.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Use o PowerShell toocreate uma disponibilidade definida
Este exemplo cria um conjunto nomeada de disponibilidade **myAvailabilitySet** em Olá **myResourceGroup** grupo de recursos em Olá **Oeste dos EUA** local. Isso deve toobe feito antes de criar hello primeira VM que estarão no conjunto de saudação.

Antes de começar, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


Se você estiver usando Managed Disks para suas VMs, digite:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Se você estiver usando suas próprias contas de armazenamento para suas VMs, digite:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Para obter mais informações, consulte [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Solucionar problemas
* Quando você cria uma máquina virtual, se conjunto de disponibilidade de saudação desejado não estiver na lista suspensa de saudação no portal de saudação você pode criá-lo em outro grupo de recursos. Se você não souber o grupo de recursos de saudação de disponibilidade do seu conjunto, acesse o menu de hub toohello e clique em Procurar > toosee define uma lista de sua disponibilidade e quais grupos de recursos que pertençam a conjuntos de disponibilidade.

## <a name="next-steps"></a>Próximas etapas
Adicionar armazenamento adicional tooyour VM adicionando mais [disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

