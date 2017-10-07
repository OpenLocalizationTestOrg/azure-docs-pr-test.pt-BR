---
title: interface de rede tooreset aaaHow para VM do Windows Azure | Microsoft Docs
description: Mostra como tooreset interface de rede de VM do Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Como tooreset interface de rede de VM do Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Não é possível conectar tooMicrosoft Windows Máquina Virtual (VM) do Azure depois de desabilitar o padrão de saudação de rede (NIC) ou manualmente define um endereço IP estático para a NIC hello. Este artigo mostra como tooreset Olá interface de rede de VM do Windows Azure, que resolverá o problema de conexão remota hello.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Redefinir o adaptador de rede

### <a name="for-classic-vms"></a>Para VMs Clássicas

rede tooreset interface, siga estas etapas:

1.  Vá toohello [portal do Azure]( https://ms.portal.azure.com).
2.  Selecione **Máquinas Virtuais (Clássicas)**.
3.  Selecione Olá afetados Máquina Virtual.
4.  Selecione **Endereços IP**.
5.  Se hello **atribuição de IP privado** não é **estático**, alterá-la muito**estático**.
6.  Saudação de alteração **endereço IP** tooanother endereço IP que está disponível no hello sub-rede.
7.  Selecione Salvar.
8.  máquina virtual de saudação reiniciará tooinitialize Olá novo NIC toohello sistema.
9.  Tente tooRDP tooyour máquina. Se for bem-sucedido, você pode alterar Olá toohello voltar de endereço de IP privado original se você quiser. Caso contrário, você poderá mantê-lo. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Para as VMs implantadas no modelo de Grupo de recursos

1.  Vá toohello [portal do Azure]( https://ms.portal.azure.com).
2.  Selecione Olá afetados Máquina Virtual.
3.  Selecione **Adaptadores de Rede**.
4.  Selecione Olá associado à Interface de rede com sua máquina
5.  Selecione **Configurações de IP**.
6.  Selecione IP hello. 
7.  Se hello **atribuição de IP privado** não é **estático**, alterá-la muito**estático**.
8.  Saudação de alteração **endereço IP** tooanother endereço IP que está disponível no hello sub-rede.
9. máquina virtual de saudação reiniciará tooinitialize Olá novo NIC toohello sistema.
10. Tente tooRDP tooyour máquina. Se for bem-sucedido, você pode alterar Olá toohello voltar de endereço de IP privado original se você quiser. Caso contrário, você poderá mantê-lo. 

## <a name="delete-hello-unavailable-nics"></a>Excluir Olá NICs indisponíveis
Depois que você pode máquina toohello de área de trabalho remota, você deve excluir Olá antigo NICs tooavoid Olá problema em potencial:

1.  Abra o Gerenciador de Dispositivos.
2.  Selecione **Exibir** > **Mostrar dispositivos ocultos**.
3.  Selecione **Adaptadores de Rede**. 
4.  Verifique se há adaptadores Olá nomeadas como "Adaptador de rede do Microsoft Hyper-V".
5.  Talvez você veja um adaptador não disponível que está esmaecido. Clique com botão direito adaptador hello e, em seguida, selecione Desinstalar.

    ![imagem de saudação do hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Desinstale somente os adaptadores indisponível Olá com nome hello "Adaptador de rede do Microsoft Hyper-V". Se você desinstalar qualquer Olá outros adaptadores ocultados, isso pode causar problemas adicionais.
    >
    >

6.  Agora todos os adaptadores não disponíveis deverão ser limpos do sistema.