---
title: aaaCannot conectar-se com o RDP tooa VM do Windows no Azure | Microsoft Docs
description: "Solucionar problemas quando você não pode se conectar a máquina virtual do tooyour Windows no Azure usando a área de trabalho remota"
keywords: "Erro de área de trabalho remoto, erro de conexão de área de trabalho remota, não é possível conectar tooVM, solução de problemas da área de trabalho remota"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Solucionar problemas de conexões de área de trabalho remota tooan máquina virtual do Azure
Olá protocolo de área de trabalho remota (RDP) conexão tooyour baseados no Windows Azure máquina virtual (VM) pode falhar por várias razões, deixando-não é possível tooaccess sua VM. pode ser problema Olá Olá serviços de área de trabalho remota em Olá VM, conexão de rede de saudação ou cliente de área de trabalho remota Olá no computador host. Este artigo o orienta por meio de alguns dos problemas hello mais comuns métodos tooresolve RDP conexão. 

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Etapas rápidas para solucionar problemas
Depois de cada etapa de solução de problemas, tente reconectar-se toohello VM:

1. Redefina a configuração da Área de Trabalho Remota.
2. Verifique as regras do Grupo de Segurança de Rede/de pontos de extremidade dos Serviços de Nuvem.
3. Examine os logs do console da VM.
4. Saudação de redefinição de NIC para Olá VM.
5. Saudação de verificação de integridade de recursos da VM.
6. Redefina a senha da VM.
7. Reinicie a VM.
8. Reimplante a VM.

Caso você precise de etapas e explicações mais detalhadas, continue lendo. Verifique se equipamentos de rede local, como roteadores e firewalls, não estão bloqueando a porta de saída TCP 3389, conforme observado nos [cenários detalhados de solução de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Se hello **conectar** botão para sua VM ficará cinza no portal de saudação e você não estiver conectado tooAzure por meio de um [rota expressa](../../expressroute/expressroute-introduction.md) ou [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexão, é necessário toocreate e atribuir sua VM um IP público endereço antes de você podem usar RDP. Leia mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Problemas de RDP de maneiras tootroubleshoot
Você pode solucionar problemas de máquinas virtuais criadas usando o modelo de implantação do Gerenciador de recursos de saudação usando um dos métodos a seguir de saudação:

* [Portal do Azure](#using-the-azure-portal) - ótimo se você precisar tooquickly redefinir as credenciais de usuário ou configurações de RDP hello e você não tiver instaladas as ferramentas do Azure hello.
* [O Azure PowerShell](#using-azure-powershell) - se você estiver familiarizado com um prompt do PowerShell, rapidamente redefinição Olá RDP configuração ou credenciais do usuário usando os cmdlets do PowerShell do Azure hello.

Você também pode encontrar etapas sobre como solucionar problemas de máquinas virtuais criadas usando Olá [modelo de implantação clássico](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Solucionar problemas usando Olá portal do Azure
Depois de cada etapa de solução de problemas, tente conectar-se tooyour VM novamente. Se você ainda não é possível se conectar, tente Olá próxima etapa.

1. **Redefina a conexão RDP**. Essa etapa de solução de problemas redefine a configuração de RDP hello quando conexões remotas estão desabilitadas ou regras de Firewall do Windows estão bloqueando o RDP, por exemplo.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **Redefinir senha** botão. Saudação de conjunto **modo** muito**apenas a configuração de redefinição** e, em seguida, clique em Olá **atualização** botão:
   
    ![Redefinir a configuração de RDP Olá no hello portal do Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Verifique as regras de Grupo de Segurança de Rede**. Use [Verifique se o fluxo IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm se uma regra em um grupo de segurança de rede está bloqueando o tráfego tooor de uma máquina virtual. Você também pode analisar as regras de entrada tooensure "Permitir" NSG regra existe e é priorizada para a porta do RDP (padrão 3389) do grupo de segurança efetiva. Para obter mais informações, consulte [fluxo de tráfego usando regras de segurança efetiva tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Examine o diagnóstico de inicialização da VM**. Essa etapa de solução de problemas revisa Olá VM console logs toodetermine se Olá VM está relatando um problema. Nem todas as VMs têm diagnóstico de inicialização habilitado, portanto, essa etapa de solução de problemas pode ser opcional.
   
    Etapas de solução de problemas específicas estão além do escopo deste artigo hello, mas podem indicar um problema maior que está afetando a conectividade RDP. Para obter mais informações sobre como analisar logs do console hello e captura de tela de VM, consulte [diagnósticos de inicialização para máquinas virtuais](boot-diagnostics.md).

4. **Saudação de redefinição de NIC para Olá VM**. Para obter mais informações, consulte [como tooreset NIC para VM do Windows Azure](reset-network-interface.md).
5. **Verificar Olá integridade de recursos da VM**. Essa etapa de solução de problemas verifica não existem problemas conhecidos com hello plataforma Windows Azure que pode afetar a conectividade toohello VM.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **integridade de recursos** botão. Uma VM íntegra é reportada como estando **Disponível**:
   
    ![Verifique a integridade do recurso VM no portal do Azure de saudação](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Redefina as credenciais do usuário**. Essa etapa de solução de problemas redefine a senha de saudação em uma conta de administrador local quando você não tiver certeza ou tiver esquecido credenciais hello.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **Redefinir senha** botão. Verifique se Olá **modo** está definido muito**Redefinir senha** e, em seguida, digite seu nome de usuário e uma nova senha. Por fim, clique em Olá **atualização** botão:
   
    ![Redefinir credenciais de usuário de saudação em Olá portal do Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Reinicie a VM**. Essa etapa de solução de problemas pode corrigir os problemas subjacentes Olá própria máquina virtual está tendo.
   
    Selecione a VM no portal do Azure de saudação e clique em Olá **visão geral** guia. Clique em Olá **reiniciar** botão:
   
    ![Reiniciar Olá VM Olá portal do Azure](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Reimplante a VM**. Essa etapa de solução de problemas reimplanta o host de tooanother VM no Azure toocorrect problemas de rede ou a plataforma subjacentes.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **reimplantar** botão e, em seguida, clique em **reimplantar**:
   
    ![Reimplantar Olá VM em Olá portal do Azure](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Após concluir essa operação, dados disco efêmera são perdidos e dinâmicos endereços IP que estão associados a saudação VM são atualizadas.

Caso ainda esteja tendo problemas de RDP, você poderá [abrir uma solicitação](https://azure.microsoft.com/support/options/) de suporte ou ler [conceitos e etapas de solução de problemas de RDP mais detalhados](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Solucionar problemas usando o Azure PowerShell
Se você ainda não o fez, [instalar e configurar hello Azure PowerShell mais recente](/powershell/azure/overview).

Olá exemplos a seguir usam variáveis como `myResourceGroup`, `myVM`, e `myVMAccessExtension`. Substitua essas localizações e nomes de variáveis por seus próprios valores.

> [!NOTE]
> Redefinir credenciais de usuário hello e configuração de RDP hello usando Olá [AzureRmVMAccessExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet do PowerShell. Em Olá seguindo exemplos `myVMAccessExtension` é um nome que você especificar como parte do processo de saudação. Caso você tenha trabalhado anteriormente com hello VMAccessAgent, você pode obter o nome de saudação de extensão existente hello usando `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck propriedades Olá Olá VM. nome do hello tooview, procure na seção de extensões' hello' de saída de hello.

Depois de cada etapa de solução de problemas, tente conectar-se tooyour VM novamente. Se você ainda não é possível se conectar, tente Olá próxima etapa.

1. **Redefina a conexão RDP**. Essa etapa de solução de problemas redefine a configuração de RDP hello quando conexões remotas estão desabilitadas ou regras de Firewall do Windows estão bloqueando o RDP, por exemplo.
   
    exemplo Hello a seguir redefine a conexão de RDP de saudação em uma VM denominada `myVM` em Olá `WestUS` local e no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Verifique as regras de Grupo de Segurança de Rede**. Essa etapa de solução de problemas verifica se você tem uma regra em seu tráfego do grupo de segurança de rede toopermit RDP. porta padrão de saudação para RDP é a porta TCP 3389. Tráfego RDP de toopermit uma regra não pode ser criado automaticamente quando você cria a VM.
   
    Atribuir pela primeira vez, todos os dados de configuração de Olá para o grupo de segurança de rede toohello `$rules` variável. Olá, exemplo a seguir obtém informações sobre Olá grupo de segurança de rede denominado `myNetworkSecurityGroup` no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Agora, Olá regras de exibição que estão configuradas para esse grupo de segurança de rede. Verifique se existe uma regra tooallow a porta TCP 3389 para conexões de entrada da seguinte maneira:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Olá, exemplo a seguir mostra uma regra de segurança válido que permite o tráfego RDP. Você pode ver que `Protocol`, `DestinationPortRange`, `Access` e `Direction` estão configuradas corretamente:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Se você não tiver uma regra que permita o tráfego RDP, deverá [criar uma regra de Grupo de Segurança de Rede](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Permita a porta TCP 3389.
3. **Redefina as credenciais do usuário**. Essa etapa de solução de problemas redefine a senha de saudação na conta de administrador local Olá especificado quando você não tiver certeza da ou tiver esquecido, credenciais de saudação.
   
    Primeiro, especifique Olá nome de usuário e uma nova senha atribuindo credenciais toohello `$cred` variável da seguinte maneira:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Agora, atualize as credenciais de saudação na sua VM. Olá, exemplo a seguir atualiza as credenciais de saudação em uma VM denominada `myVM` em Olá `WestUS` local e no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Reinicie a VM**. Essa etapa de solução de problemas pode corrigir os problemas subjacentes Olá própria máquina virtual está tendo.
   
    Olá reinicializações de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Reimplante a VM**. Essa etapa de solução de problemas reimplanta o host de tooanother VM no Azure toocorrect problemas de rede ou a plataforma subjacentes.
   
    Olá reimplanta de exemplo a seguir Olá VM denominada `myVM` em Olá `WestUS` local e no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Caso ainda esteja tendo problemas de RDP, você poderá [abrir uma solicitação](https://azure.microsoft.com/support/options/) de suporte ou ler [conceitos e etapas de solução de problemas de RDP mais detalhados](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Solucionar problemas de máquinas virtuais criadas usando o modelo de implantação clássico Olá
Depois de cada etapa de solução de problemas, tente reconectar-se toohello VM.

1. **Redefina a conexão RDP**. Essa etapa de solução de problemas redefine a configuração de RDP hello quando conexões remotas estão desabilitadas ou regras de Firewall do Windows estão bloqueando o RDP, por exemplo.
   
    Selecione a VM em Olá portal do Azure. Clique em Olá **... Mais** e clique em **acesso remoto redefinir**:
   
    ![Redefinir a configuração de RDP Olá no hello portal do Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Verifique os pontos de extremidade dos Serviços de Nuvem**. Essa etapa de solução de problemas verifica se você tem pontos de extremidade em seu tráfego RDP de toopermit de serviços de nuvem. porta padrão de saudação para RDP é a porta TCP 3389. Tráfego RDP de toopermit uma regra não pode ser criado automaticamente quando você cria a VM.
   
   Selecione a VM em Olá portal do Azure. Clique em Olá **pontos de extremidade** botão tooview Olá os pontos de extremidade atualmente configurados para sua VM. Verifique se existem pontos de extremidade que permitem o tráfego RDP na porta TCP 3389.
   
   saudação de exemplo a seguir mostra os pontos de extremidade válidos que permitem o tráfego RDP:
   
   ![Verifique se os pontos de extremidade de serviços de nuvem no hello portal do Azure](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Se você não tiver um ponto de extremidade que permita o tráfego RDP, deverá [criar um ponto de extremidade dos Serviços de Nuvem](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Permitir o TCP tooprivate porta 3389.
3. **Examine o diagnóstico de inicialização da VM**. Essa etapa de solução de problemas revisa Olá VM console logs toodetermine se Olá VM está relatando um problema. Nem todas as VMs têm diagnóstico de inicialização habilitado, portanto, essa etapa de solução de problemas pode ser opcional.
   
    Etapas de solução de problemas específicas estão além do escopo deste artigo hello, mas podem indicar um problema maior que está afetando a conectividade RDP. Para obter mais informações sobre como analisar logs do console hello e captura de tela de VM, consulte [diagnósticos de inicialização para máquinas virtuais](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Verificar Olá integridade de recursos da VM**. Essa etapa de solução de problemas verifica não existem problemas conhecidos com hello plataforma Windows Azure que pode afetar a conectividade toohello VM.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **integridade de recursos** botão. Uma VM íntegra é reportada como estando **Disponível**:
   
    ![Verifique a integridade do recurso VM no portal do Azure de saudação](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Redefina as credenciais do usuário**. Essa etapa de solução de problemas redefine a senha de saudação na conta de administrador local Olá que você especifique quando você não tiver certeza ou tiver esquecido credenciais hello.
   
    Selecione a VM em Olá portal do Azure. Role para baixo Olá configurações painel toohello **suporte + solução de problemas** seção inferior da lista de saudação. Clique em Olá **Redefinir senha** botão. Insira seu nome de usuário e uma nova senha. Por fim, clique em Olá **salvar** botão:
   
    ![Redefinir credenciais de usuário de saudação em Olá portal do Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Reinicie a VM**. Essa etapa de solução de problemas pode corrigir os problemas subjacentes Olá própria máquina virtual está tendo.
   
    Selecione a VM no portal do Azure de saudação e clique em Olá **visão geral** guia. Clique em Olá **reiniciar** botão:
   
    ![Reiniciar Olá VM Olá portal do Azure](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Caso ainda esteja tendo problemas de RDP, você poderá [abrir uma solicitação](https://azure.microsoft.com/support/options/) de suporte ou ler [conceitos e etapas de solução de problemas de RDP mais detalhados](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Solucionar problemas de erros de RDP específicos
Você pode encontrar uma mensagem de erro específica ao tentar tooconnect tooyour VM por meio do RDP. Olá seguem mensagens de erro mais comuns da saudação:

* [sessão remota Olá foi desconectada porque não há nenhum tooprovide de servidores de licenças de área de trabalho remota disponível uma licença](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Área de trabalho remota não é possível encontrar hello "nome do computador"](troubleshoot-specific-rdp-errors.md#rdpname).
* [Ocorreu um erro de autenticação. Olá autoridade de segurança Local não pode ser contatada](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Erro de Segurança do Windows: suas credenciais não funcionaram](troubleshoot-specific-rdp-errors.md#wincred).
* [Este computador não é possível conectar o computador remoto toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Recursos adicionais
Se nenhum desses erros ocorreram e você não pode conectar toohello VM por meio da área de trabalho remota, leia Olá detalhada [guia para a área de trabalho remota de solução de problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para solucionar problemas de etapas ao acessar aplicativos em execução em uma máquina virtual, consulte [aplicativo de tooan acesso de solução de problemas em execução em uma VM do Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Se você estiver tendo problemas para usar o Secure Shell (SSH) tooconnect tooa VM do Linux no Azure, consulte [solucionar problemas de SSH conexões tooa VM do Linux no Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

