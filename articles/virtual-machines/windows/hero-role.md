---
title: aaaInstall IIS em sua primeira VM do Windows | Microsoft Docs
description: "Testar sua primeira máquina virtual do Windows instalando o IIS e abrindo a porta 80 usando Olá portal do Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Experimentar a instalação de uma função em sua VM do Windows
Uma vez que a sua primeira máquina virtual (VM) para cima e em execução, você pode mover tooinstalling softwares e serviços. Para este tutorial, vamos toouse Gerenciador do servidor em Olá tooinstall de VM do Windows Server IIS. Em seguida, vamos criar um grupo de segurança de rede (NSG) usando o tráfego do hello tooopen portal do Azure na porta 80 tooIIS. 

Se você ainda não criou sua primeira VM, você deverá voltar muito[criar sua primeira máquina virtual do Windows no portal do Azure de saudação](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar com este tutorial.

## <a name="make-sure-hello-vm-is-running"></a>Verifique se Olá que VM está em execução
1. Olá abrir [portal do Azure](https://portal.azure.com).
2. No menu de hub hello, clique em **máquinas virtuais**. Selecione máquina virtual de Olá Olá lista.
3. Se o status de saudação é **parado (desalocado)**, clique Olá **iniciar** botão Olá **Essentials** folha de saudação VM. Se o status de saudação é **executando**, você pode mover toohello próxima etapa.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Conecte-se a máquina virtual de toohello e entrar
1. No menu de hub hello, clique em **máquinas virtuais**. Selecione máquina virtual de Olá Olá lista.
2. Na folha de saudação para a máquina virtual de saudação, clique em **conectar**. Isso cria e baixa um arquivo de protocolo de área de trabalho remota (arquivo. rdp) que é como uma máquina de tooyour de tooconnect de atalho. Talvez você queira área de trabalho do toosave Olá arquivo tooyour para facilitar o acesso. **Abra** tooyour de tooconnect este arquivo VM.
   
    ![Captura de tela da saudação mostrando portal do Azure como tooconnect tooyour VM](./media/hero-role/connect.png)
3. Você receberá um aviso que. rdp de saudação for de um editor desconhecido. Isso é normal. Na janela de área de trabalho remota hello, clique em **conectar** toocontinue.
   
    ![Captura de tela de um aviso sobre um editor desconhecido](./media/hero-role/rdp-warn.png)
4. Na janela de segurança do Windows hello, nome de usuário do tipo hello e a senha da conta de local de saudação que é criada quando você criou Olá VM. nome de usuário de saudação é inserido como *vmname*&#92; *nome de usuário*, em seguida, clique em **Okey**.
   
    ![Captura de tela de inserir o nome da VM Olá, nome de usuário e senha](./media/hero-role/credentials.png)
5. Receber um aviso de certificado Olá não pode ser verificado. Isso é normal. Clique em **Sim** tooverify Olá identidade da máquina virtual de saudação e concluir o registro em log.
   
   ![Captura de tela mostrando uma mensagem limitam a verificar a identidade de saudação do hello VM](./media/hero-role/cert-warning.png)

Se você executar tootrouble quando você tentar tooconnect, consulte [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Instalar o IIS em sua VM
Agora que você está logado toohello VM, vamos instalar uma função de servidor para que você possa testar mais.

1. Abra o **Gerenciador de Servidores** se ainda não estiver aberto. Clique em Olá **iniciar** menu e clique **Gerenciador do servidor**.
2. Em **Gerenciador do servidor**, selecione **servidor Local** no painel esquerdo do hello. 
3. No menu de saudação, selecione **gerenciar** > **adicionar funções e recursos**.
4. Em Olá assistente Adicionar funções e recursos, em Olá **tipo de instalação** escolha **instalação baseada em função ou recurso**e, em seguida, clique em **próximo**.
   
    ![Captura de tela mostrando Olá assistente Adicionar funções e recursos de guia para o tipo de instalação](./media/hero-role/role-wizard.png)
5. Selecione Olá VM do pool de saudação do servidor e clique em **próximo**.
6. Em Olá **funções de servidor** página, selecione **servidor Web (IIS)**.
   
    ![Captura de tela mostrando Olá assistente Adicionar funções e recursos do guia de funções de servidor](./media/hero-role/add-iis.png)
7. No hello pop-up sobre como adicionar recursos necessários para o IIS, verifique se **incluir ferramentas de gerenciamento** está selecionado e, em seguida, clique em **adicionar recursos**. Quando fecha Olá pop-up, clique em **próximo** no Assistente de saudação.
   
    ![Captura de tela mostrando tooconfirm pop-up, adicionando a função do IIS Olá](./media/hero-role/confirm-add-feature.png)
8. Na página de recursos de saudação, clique em **próximo**.
9. Em Olá **função de servidor Web (IIS)** , clique em **próximo**. 
10. Em Olá **serviços de função** , clique em **próximo**. 
11. Em Olá **confirmação** , clique em **instalar**. 
12. Quando a saudação instalação for concluída, clique em **fechar** no Assistente de saudação.

## <a name="open-port-80"></a>Abrir a porta 80
Para que sua VM tooaccept o tráfego de entrada pela porta 80, é necessário tooadd um grupo de segurança de rede de toohello regra de entrada. 

1. Olá abrir [portal do Azure](https://portal.azure.com).
2. Em **máquinas virtuais** selecione Olá VM que você criou.
3. Em configurações de máquinas virtuais hello, selecione **interfaces de rede** e, em seguida, selecione Olá interface de rede existente.
   
    ![Captura de tela mostrando a configuração de máquina virtual de saudação para Olá interfaces de rede](./media/hero-role/network-interface.png)
4. Em **Essentials** Olá interface de rede, clique em Olá **grupo de segurança de rede**.
   
    ![Captura de tela mostrando a seção do Essentials Olá Olá interface de rede](./media/hero-role/select-nsg.png)
5. Em Olá **Essentials** folha para Olá NSG, você deve ter um padrão existente regra de entrada de **rdp permitir padrão** que permite que você toolog em toohello VM. Adicione outro tráfego IIS tooallow de regra de entrada. Clique em **Regra de segurança de entrada**.
   
    ![Captura de tela mostrando a seção Essentials Olá Olá NSG](./media/hero-role/inbound.png)
6. Nas **Regras de segurança de entrada**, clique em **Adicionar**.
   
    ![Captura de tela mostrando Olá botão tooadd uma regra de segurança](./media/hero-role/add-rule.png)
7. Nas **Regras de segurança de entrada**, clique em **Adicionar**. Tipo **80** em Olá intervalo de portas e certifique-se de **permitir** está selecionado. Quando terminar, clique em **OK**.
   
    ![Captura de tela mostrando Olá botão tooadd uma regra de segurança](./media/hero-role/port-80.png)

Para obter mais informações sobre os NSGs, regras de entrada e saída, consulte [permitir acesso externo tooyour VM usando Olá portal do Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Conecte-se o site do IIS padrão toohello
1. No portal do Azure de Olá, clique em **máquinas virtuais** e, em seguida, selecione a VM.
2. Em Olá **Essentials** folha, copie o **endereço IP público**.
   
    ![Captura de tela mostrando onde toofind Olá endereço IP público da VM](./media/hero-role/ipaddress.png)
3. Abra um navegador e na barra de endereços do hello, digite em seu endereço IP público como este: http://<publicIPaddress> e clique em **Enter** toogo toothat endereço.
4. Seu navegador deve abrir a página de web IIS saudação padrão. É algo semelhante a isto:
   
    ![Captura de tela mostrando qual página IIS padrão Olá aparência em um navegador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Próximas etapas
* Você também pode fazer experiências com [anexar um disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour VM. Os discos de dados oferecem mais armazenamento para sua máquina virtual.

