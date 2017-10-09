---
title: aaaReset uma senha local do Windows sem agente do Azure | Microsoft Docs
description: "Como tooreset Olá a senha de uma conta de usuário do Windows local quando o agente de convidado do Azure Olá não está instalado ou funcionando em uma máquina virtual"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Como tooreset senha do Windows local para a máquina virtual do Azure
Você pode redefinir senha do Windows local saudação de uma VM no Azure usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) desde que o agente de convidado do Azure hello está instalado. Esse método é Olá principal maneira tooreset uma senha para uma VM do Azure. Se você tiver problemas com o agente de convidado do Azure Olá não está respondendo ou falhando tooinstall depois de carregar uma imagem personalizada, você pode redefinir manualmente uma senha do Windows. Este artigo fornece detalhes sobre como tooreset uma senha de conta local, anexando Olá tooanother de disco virtual de origem SO VM. 

> [!WARNING]
> Use esse processo apenas como último recurso. Tente tooreset sempre uma senha usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primeiro.
> 
> 

## <a name="overview-of-hello-process"></a>Visão geral do processo de saudação
etapas de núcleo Olá para executar uma redefinição para uma VM do Windows Azure quando não há nenhum agente de convidado do Azure toohello acesso de senha local é o seguinte:

* Exclua VM de origem hello. discos virtuais Olá são mantidos.
* Anexar tooanother disco de sistema operacional da VM de origem Olá VM em Olá mesmo local dentro de sua assinatura do Azure. Essa VM é chamado tooas Olá VM de solução de problemas.
* Usando Olá VM de solução de problemas, crie alguns arquivos de configuração no disco do sistema operacional da VM de origem hello.
* Desanexe o disco do sistema operacional da VM de saudação do hello VM de solução de problemas.
* Use um modelo de Gerenciador de recursos toocreate uma VM, usando o disco virtual original de saudação.
* Quando a nova VM é inicializado, Olá Olá arquivos de configuração cria Olá de atualização de senha do usuário Olá necessário.

## <a name="detailed-steps"></a>Etapas detalhadas
Tente tooreset sempre uma senha usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de tentar Olá etapas a seguir. Verifique se você tem um backup da VM antes de iniciar. 

1. Excluir Olá afetados VM no portal do Azure. Excluindo Olá VM exclui somente metadados hello, referência de saudação do hello VM no Azure. discos virtuais Olá são mantidos quando Olá VM é excluída:
   
   * Selecione Olá VM em Olá portal do Azure, clique em *excluir*:
     
     ![Excluir VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. Anexe toohello de disco do sistema operacional da VM de origem Olá VM de solução de problemas. Olá Solucionando problemas de VM deve estar no hello mesma região que o disco do sistema operacional da VM de origem hello (como `West US`):
   
   * Selecione Olá VM de solução de problemas no hello portal do Azure. Clique em *Discos* | *Anexar existente*:
     
     ![Anexar disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Selecione *arquivo VHD* e, em seguida, selecione conta de armazenamento de saudação que contém seu VM de origem:
     
     ![Escolher conta de armazenamento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Selecione o recipiente de origem hello. contêiner de origem Olá normalmente é *vhds*:
     
     ![Escolher contêiner de armazenamento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Selecione Olá tooattach de vhd de sistema operacional. Clique em *selecione* toocomplete processo de saudação:
     
     ![Escolher o disco virtual de origem](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Conecte-se toohello VM usando a área de trabalho remota de solução de problemas e certifique-se de disco do sistema operacional da VM de origem Olá é visível:
   
   * Selecione Olá VM de solução de problemas no hello portal do Azure e clique em *conectar*.
   * Abrir arquivo RDP Olá que baixa. Insira a saudação de nome de usuário e a senha da saudação VM de solução de problemas.
   * No Explorador de arquivos, procure o disco de dados Olá anexado. Se hello fonte que VHD da VM é hello somente os dados em disco anexado toohello VM de solução de problemas, ele deverá ser unidade f: de saudação:
     
     ![Exibir o disco de dados anexado](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Criar `gpt.ini` em `\Windows\System32\GroupPolicy` na unidade da VM de origem hello (se existir gpt.ini, renomeie toogpt.ini.bak):
   
   > [!WARNING]
   > Certifique-se de não acidentalmente criar hello seguintes arquivos em C:\Windows, Olá unidade do sistema operacional para Olá VM de solução de problemas. Crie hello seguintes arquivos na unidade de saudação SO para sua VM que está anexado como um disco de dados de origem.
   > 
   > 
   
   * Adicionar Olá linhas seguintes no hello `gpt.ini` arquivo criado:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Criar gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Crie `scripts.ini` em `\Windows\System32\GroupPolicy\Machine\Scripts`. Verifique se as pastas ocultas são mostradas. Se necessário, crie Olá `Machine` ou `Scripts` pastas.
   
   * Adicionar Olá Olá linhas a seguir `scripts.ini` arquivo criado:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Criar scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Criar `FixAzureVM.cmd` na `\Windows\System32` com hello conteúdo a seguir, substituindo `<username>` e `<newpassword>` com seus próprios valores:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Criar FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Você deve atender aos requisitos de complexidade de senha Olá configurado para sua VM ao definir a nova senha de saudação.
7. No portal do Azure, Desanexe o disco de saudação do hello VM de solução de problemas:
   
   * Selecione Olá VM de solução de problemas no hello portal do Azure, clique em *discos*.
   * Disco de dados selecione Olá anexado na etapa 2, clique em *desanexar*:
     
     ![Desanexar disco](./media/reset-local-password-without-agent/detach_disk.png)
8. Antes de criar uma máquina virtual, obtenha o disco do sistema operacional de origem do hello URI tooyour:
   
   * Conta de armazenamento selecione Olá Olá portal do Azure, clique em *Blobs*.
   * Selecione o contêiner de saudação. contêiner de origem Olá normalmente é *vhds*:
     
     ![Selecionar o blob da conta de armazenamento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Selecione a fonte de VHD de sistema operacional da máquina virtual e clique em Olá *cópia* toohello próximo botão *URL* nome:
     
     ![Copiar URI do disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Crie uma máquina virtual do disco do sistema operacional da VM de origem hello:
   
   * Use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate uma VM em um VHD especializada. Clique em Olá `Deploy tooAzure` saudação do botão tooopen portal do Azure com os detalhes do modelo Olá preenchido para você.
   * Se você desejar tooretain todas as configurações anteriores de saudação para Olá VM, selecione *Editar modelo* tooprovide sua rede virtual existente, sub-rede, adaptador de rede ou IP público.
   * Em Olá `OSDISKVHDURI` caixa de texto de parâmetro, Olá colar URI de sua fonte de VHD obter Olá anterior etapa:
     
     ![Criar uma VM usando o modelo](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Após Olá nova máquina virtual está em execução, conecte-se toohello VM usando a área de trabalho remota com hello a nova senha especificada no hello `FixAzureVM.cmd` script.
11. Na sua sessão remota toohello nova VM, Olá remove a seguir arquivos tooclean ambiente hello:
    
    * De %windir%\System32
      * remova FixAzureVM.cmd
    * De %windir%\System32\GroupPolicy\Machine\
      * remova scripts.ini
    * De %windir%\System32\GroupPolicy
      * Remover gpt.ini (se gpt.ini existia antes, e você renomeou toogpt.ini.bak, renomeação hello. bak arquivo back toogpt.ini)

## <a name="next-steps"></a>Próximas etapas
Se você ainda não é possível se conectar usando a área de trabalho remota, consulte Olá [guia de solução de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Olá [detalhadas RDP guia de solução de problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examina métodos em vez de etapas específicas de solução de problemas. Você também pode [abrir uma solicitação de suporte do Azure](https://azure.microsoft.com/support/options/) para obter assistência prática.

