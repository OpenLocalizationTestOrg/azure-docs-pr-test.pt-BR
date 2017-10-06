---
title: aaaConfigure uma rede virtual no Azure DevTest Labs | Microsoft Docs
description: "Saiba como tooconfigure uma rede virtual existente e a sub-rede e usá-los em uma VM com o Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Configurar uma rede virtual no Azure DevTest Labs
Conforme explicado no artigo hello, [adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md), quando você cria uma VM em um laboratório, você pode especificar uma rede virtual configurada. Um cenário para fazer isso é se você precisar tooaccess seus recursos de rede corporativa de suas VMs usando Olá rede virtual que foi configurado com a rota expressa ou VPN site a site. Olá seções a seguir ilustram como tooadd sua rede virtual existente nas configurações de rede Virtual do laboratório para que ela seja toochoose disponível ao criar máquinas virtuais.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Configurar uma rede virtual para um laboratório com hello portal do Azure
Olá etapas a seguir orientam na adição de um laboratório de tooa rede (e subrede) de virtual existente para que ele pode ser usado ao criar uma VM em Olá mesmo laboratório. 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello. 
4. Na folha do laboratório hello, selecione **configuração**.
5. No laboratório de saudação **configuração** folha, selecione **redes virtuais**.
6. Em Olá **redes virtuais** folha, verá uma lista de redes virtuais configuradas para o laboratório atual hello, bem como saudação padrão rede virtual que é criado para o laboratório. 
7. Selecione **+ Adicionar**.
   
    ![Adicionar um laboratório de tooyour de rede virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Em Olá **rede Virtual** folha, selecione **[Selecione rede virtual]**.
   
    ![Selecionar uma rede virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Em Olá **rede virtual escolha** folha, a rede virtual desejado de saudação select. folha Hello mostra todas as redes virtuais Olá que estão em Olá mesmo região na assinatura Olá laboratório hello.  
10. Depois de selecionar uma rede virtual, você retornará toohello **rede Virtual** clique Olá sub-rede na lista de saudação na parte inferior da saudação da folha de saudação.

    ![Lista de sub-redes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    folha de sub-rede do laboratório de saudação é exibida.

    ![Folha Sub-rede do laboratório](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Especifique um **nome da Sub-rede do laboratório**.
12. tooallow um toobe sub-rede usada no laboratório de criação de VM, selecione **uso na criação da máquina virtual**.
13. tooenable um [compartilhado endereço IP público](devtest-lab-shared-ip.md), selecione **habilitar compartilhada IP público**.
14. Selecione tooallow de endereços IP públicos em uma sub-rede, **permitir a criação de IP pública**.
15. Em Olá **máximo de máquinas virtuais por usuário** , especifique Olá VMs máximo por usuário para cada sub-rede. Se você quiser um número irrestrito de VMs, deixe esse campo em branco.
16. Selecione **Okey** tooclose folha de sub-rede do laboratório de saudação.
17. Selecione **salvar** folha de rede tooclose Olá Virtual.
18. Hello rede virtual já está configurado, ele pode ser selecionado durante a criação de uma máquina virtual. 
    toosee como toocreate uma máquina virtual e especifique uma rede virtual, consulte o artigo toohello, [adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Depois que você adicionou a saudação desejado laboratório tooyour de rede virtual, a próxima etapa de saudação é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).

