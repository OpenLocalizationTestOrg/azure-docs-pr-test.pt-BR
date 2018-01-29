---
title: "Solucionar um problema de VM do Azure usando a virtualização aninhada no Azure | Microsoft Docs"
description: "Como solucionar um problema de VM do Azure usando a virtualização aninhada no Azure"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 11/06/2017
ms.author: genli
ms.openlocfilehash: b50d139f62ef773fb5b9bb2638e40f8154e80979
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2018
---
# <a name="troubleshoot-a-problem-azure-vm-by-using-nested-virtualization-in-azure"></a>Solucionar um problema de VM do Azure usando a virtualização aninhada no Azure

Este artigo mostra como criar um ambiente de virtualização aninhado no Microsoft Azure, portanto você pode montar o disco da VM com problema no host Hyper-V (VM de Recuperação) para fins de solução de problemas.

## <a name="prerequisite"></a>Pré-requisito

Para montar VM com problema, a VM de recuperação deve atender aos seguintes pré-requisitos:

-   A VM de recuperação deve estar no mesmo local que a VM com problema.

-   A VM de recuperação deve estar no mesmo grupo de recursos que a VM com problema.

-   A VM de recuperação deve usar o mesmo tipo de conta de armazenamento (Standard ou Premium) que a VM com problema.

## <a name="step-1-create-a-recovery-vm-and-install-hyper-v-role"></a>Etapa 1: criar uma VM de recuperação e instalar a função Hyper-V

1.  Crie uma nova VM de recuperação:

    -  Sistema operacional: Windows Server 2016 Datacenter

    -  Tamanho: qualquer série V3 com pelo menos dois núcleos que dão suporte à virtualização aninhada. Para obter mais informações, consulte [Introdução aos novos tamanhos de VM Dv3 e Ev3](https://azure.microsoft.com/blog/introducing-the-new-dv3-and-ev3-vm-sizes/).

    -  Mesmo local, conta de armazenamento e o grupo de recursos que a VM com problema.

    -  Selecione o mesmo tipo de armazenamento da VM com problema (Standard ou Premium).

2.  Após a VM de recuperação ser criada, acesse a VM de recuperação via área de trabalho remota.

3.  No Gerenciador do Servidor, selecione **Gerenciar** > **Adicionar Funções e Recursos**.

4.  Na seção **Tipo de Instalação**, selecione **Instalação baseada em função ou recurso**.

5.  Na seção **Selecionar servidor de destino**, verifique se a VM de recuperação está selecionada.

6.  Selecione a **Função Hyper-V** > **Adicionar Recursos**.

7.  Selecione **Próximo** na seção **Recursos**.

8.  Se um comutador virtual estiver disponível, selecione-o. Caso contrário, selecione **Avançar**.

9.  Na seção **Migração**, selecione **Avançar**

10. Na seção **Repositórios Padrão**, selecione **Avançar**.

11. Marque a caixa para reiniciar o servidor automaticamente se necessário.

12. Selecione **Instalar**.

13. Permita que o servidor instale a função Hyper-V. Isso leva alguns minutos e o servidor será reiniciado automaticamente.

## <a name="step-2-create-the-problem-vm-on-the-recovery-vms-hyper-v-server"></a>Etapa 2: criar a VM com o problema no servidor Hyper-V da VM de recuperação

1.  Registre o nome do disco na VM com problema e exclua-a em seguida. Verifique se você está mantendo todos os discos anexados. 

2.  Anexe o disco do SO da VM com problema como um disco de dados da VM de recuperação.

    1.  Após a VM com problema ser excluída, vá para a VM de recuperação.

    2.  Selecione **Discos** e, em seguida, **Adicionar disco de dados**.

    3.  Selecione o disco da VM com problema e, em seguida, selecione **Salvar**.

3.  Após o disco ser anexado com êxito, conecte-se à VM de recuperação via área de trabalho remota.

4.  Abra o Disk Management (diskmgmt.msc). Verifique se o disco da VM com problema está definido como **Offline**.

5.  Abra o Gerenciador do Hyper-V: em **Gerenciador do Servidor**, selecione a **Função do Hyper-V**. Clique com o botão direito do mouse no servidor e, em seguida, selecione o **Gerenciador do Hyper-V**.

6.  No Gerenciador do Hyper-V, clique com o botão direito do mouse na VM de recuperação e, em seguida, selecione **Novo** > **Máquina Virtual** > **Avançar**.

7.  Digite um nome para a VM e, em seguida, selecione **Avançar**.

8.  Selecione **Geração 1**.

9.  Defina a memória de inicialização em 1.024 MB ou mais.

10. Se aplicável, selecione o comutador de rede do Hyper-V que foi criado. Caso contrário, vá para a próxima página.

11. Selecione **Anexar um disco rígido virtual mais tarde**.

    ![a imagem sobre a opção Anexar um disco rígido virtual posteriormente](./media/troubleshoot-vm-by-use-nested-virtualization/attach-disk-later.png)

12. Selecione **Concluir** quando a VM é criada.

13. Clique com o botão direito do mouse na VM que você criou e, em seguida, selecione **Configurações**.

14. Selecione o **Controlador IDE 0**, selecione **Disco Rígido** e, em seguida, clique em **Adicionar**.

    ![a imagem sobre adicionar novo disco rígido](./media/troubleshoot-vm-by-use-nested-virtualization/create-new-drive.png)    

15. Em **Disco Rígido Físico**, selecione o disco da VM com problema anexado à VM do Azure. Se você não vê todos os discos listados, verifique se o disco está definido como offline usando o gerenciamento de disco.

    ![a imagem sobre montar o disco](./media/troubleshoot-vm-by-use-nested-virtualization/mount-disk.png)  


17. Selecione **Aplicar** e, depois, **OK**.

18. Clique duas vezes na VM e, em seguida, inicie-a.

19. Agora você pode trabalhar na VM como a VM local. Você poderá seguir as etapas de solução de problemas que forem necessárias.

## <a name="step-3-re-create-your-azure-vm-in-azure"></a>Etapa 3: criar novamente sua VM do Azure no Azure

1.  Depois de colocar a VM novamente online, desligue-a no Gerenciador do Hyper-V.

2.  Vá para o [Portal do Azure](https://portal.azure.com), selecione a VM de Recuperação > Discos e copie o nome do disco. Você usará o nome na próxima etapa. Desanexe o disco fixo da VM de recuperação.

3.  Vá para **Todos os recursos**, pesquise pelo nome do disco e, em seguida, selecione o disco.

     ![a imagem sobre pesquisar pelo disco](./media/troubleshoot-vm-by-use-nested-virtualization/search-disk.png)     

4. Clique em **Criar VM**.

     ![a imagem sobre criar a VM do disco](./media/troubleshoot-vm-by-use-nested-virtualization/create-vm-from-vhd.png) 

Você também pode usar o Azure PowerShell para criar a VM do disco. Para obter mais informações, consulte [Criar a nova VM de um disco existente usando o PowerShell](create-vm-specialized.md#create-the-new-vm). 

## <a name="next-steps"></a>Próximas etapas

Se estiver tendo problemas para se conectar à VM, consulte [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md) (Solucionar conexões RDP a uma VM do Azure). Para problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Windows](troubleshoot-app-connection.md).
