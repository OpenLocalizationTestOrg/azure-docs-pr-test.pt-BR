---
title: "área de trabalho remota aaaDetailed de solução de problemas no Azure | Microsoft Docs"
description: "Examine as etapas detalhadas de solução de problemas para erros de área de trabalho remotas onde não é possível tooa máquinas de virtuais do Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "não é possível conectar-se a área de trabalho tooremote, solucionar problemas de área de trabalho remota, área de trabalho remota não pode se conectar, erros de área de trabalho remotos, solução de problemas da área de trabalho remota, problemas de área de trabalho remotos"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Etapas detalhadas de solução de problemas de conexão de área de trabalho remota emite tooWindows VMs no Azure
Este artigo fornece etapas de solução de problemas detalhadas toodiagnose e corrigir erros de área de trabalho remota complexos para máquinas de virtuais baseadas em Windows Azure.

> [!IMPORTANT]
> tooeliminate Olá erros mais comuns de área de trabalho remota, tooread se tornar [artigo de solução de problemas básicos Olá para área de trabalho remota](troubleshoot-rdp-connection.md) antes de continuar.

Você pode encontrar uma área de trabalho remota, mensagem de erro que não se assemelha a qualquer uma das mensagens de erro específicas Olá abordada [Olá básica área de trabalho remota guia de solução de problemas](troubleshoot-rdp-connection.md). Siga essas toodetermine etapas por que o cliente de área de trabalho remota (RDP) hello é o serviço RDP de toohello de tooconnect não é possível no hello VM do Azure.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas Frequentes de suporte do Microsoft Azure](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Componentes de uma conexão da Área de Trabalho Remota
Olá componentes a seguir é envolvido em uma conexão de RDP:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Antes de prosseguir, pode ser útil toomentally examinar o que mudou desde Olá última bem-sucedida área de trabalho remota conexão toohello VM. Por exemplo:

* Olá endereço IP público Olá VM ou saudação do serviço de nuvem que contém a saudação VM (também chamado de endereço IP virtual Olá [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) foi alterado. Olá falha RDP pode ser porque o cache do cliente DNS ainda tem Olá *endereço IP antigo* registrado para o nome DNS de saudação. Liberar o cache do cliente DNS e tente conectar-se a saudação VM novamente. Ou tente conectar-se diretamente com hello novo VIP.
* Você está usando um aplicativo de terceiros toomanage suas conexões de área de trabalho remota em vez de usar conexão Olá gerado pelo Olá portal do Azure. Verifique se que essa configuração de aplicativo hello inclui Olá correta a porta TCP para Olá tráfego de área de trabalho remota. Você pode verificar essa porta para uma máquina virtual clássica no hello [portal do Azure](https://portal.azure.com), clicando em configurações da VM hello > pontos de extremidade.

## <a name="preliminary-steps"></a>Etapas preliminares
Antes de continuar toohello solução de problemas detalhada,

* Verificar status de saudação de máquina virtual Olá Olá portal do Azure para qualquer problema óbvio.
* Siga Olá [etapas de correção rápida para erros comuns de RDP na solução de problemas básicos de saudação orientam](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Tente reconectar toohello VM por meio da área de trabalho remota após estas etapas.

## <a name="detailed-troubleshooting-steps"></a>Etapas detalhadas de solução de problemas
cliente de área de trabalho remota Olá pode não ser tooreach capaz de serviço de área de trabalho remota Olá em hello Azure VM tooissues devido a saudação as origens a seguir:

* [Computador cliente de Área de Trabalho Remota](#source-1-remote-desktop-client-computer)
* [Dispositivo de borda de intranet da organização](#source-2-organization-intranet-edge-device)
* [Ponto de extremidade de serviço de nuvem e ACL (lista de controle de acesso)](#source-3-cloud-service-endpoint-and-acl)
* [Grupos de segurança de rede](#source-4-network-security-groups)
* [VM do Azure Baseada em Windows](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Fonte 1: computador cliente de Área de Trabalho Remota
Verifique se o computador pode fazer a área de trabalho remota conexões tooanother local, o computador baseado em Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Se não for possível, verificar Olá configurações a seguir no seu computador:

* Uma configuração de firewall local que está bloqueando o tráfego de Área de Trabalho Remota.
* Um software de proxy cliente instalado localmente que está impedindo conexões de Área de Trabalho Remota.
* Um software de monitoramento de rede instalado localmente que está impedindo conexões de Área de Trabalho Remota.
* Outros tipos de software de segurança que monitoram o tráfego ou permitem/não permitem tipos específicos de tráfego e que estão impedindo conexões de Área de Trabalho Remota.

Em todos esses casos, temporariamente desabilite software hello e tente tooconnect tooan local no computador por meio da área de trabalho remota. Se você pode descobrir causa real Olá dessa maneira, trabalhe com seu administrador toocorrect Olá software configurações tooallow área de trabalho remota conexões de rede.

## <a name="source-2-organization-intranet-edge-device"></a>Fonte 2: dispositivo de borda de intranet da organização
Verifique se um computador diretamente conectado toohello que Internet pode fazer conexões de área de trabalho remota tooyour máquina virtual do Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Se você não tiver um computador que esteja conectado diretamente toohello Internet, crie e teste com uma nova máquina virtual do Azure em um serviço de nuvem ou o grupo de recursos. Para obter mais informações, consulte [Criar uma máquina virtual que executa o Windows no Azure](../virtual-machines-windows-hero-tutorial.md). Você pode excluir máquina virtual de saudação e grupo de recursos de saudação ou serviço de nuvem Olá, depois de testar a saudação.

Se você pode criar uma conexão de área de trabalho remota com um toohello computador conectado diretamente à Internet, verifique o dispositivo de borda de intranet de organização para:

* Um firewall interno bloqueando conexões de HTTPS toohello da Internet.
* Um servidor proxy impedindo conexões de Área de Trabalho Remota.
* Software de detecção de intrusão ou monitoramento de rede executado em dispositivos em sua rede de borda que está impedindo conexões de Área de Trabalho Remota.

Trabalhe com seu administrador toocorrect Olá as configurações de rede da sua organização intranet borda dispositivo tooallow área de trabalho remota com base em HTTPS conexões toohello da Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Fonte 3: ponto de extremidade de serviço de nuvem e ACL
Para máquinas virtuais criadas usando o modelo de implantação clássico hello, verifique se que outra VM do Azure que está no hello mesmo serviço de nuvem ou rede virtual pode fazer conexões de área de trabalho remota tooyour VM do Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Para máquinas virtuais criadas no Gerenciador de recursos, ignorar muito[fonte 4: grupos de segurança de rede](#source-4-network-security-groups).

Se você não tiver outra máquina virtual em Olá mesmo serviço de nuvem ou rede virtual, crie um. Siga as etapas de saudação em [criar uma máquina virtual executando o Windows Azure](../virtual-machines-windows-hero-tutorial.md). Exclua Olá máquina de virtual de teste após a conclusão do teste de saudação.

Se você puder se conectar por meio da área de trabalho remota tooa VM em hello mesmo serviço ou de rede virtual, na nuvem verificar essas configurações:

* configuração de ponto de extremidade Olá para tráfego de área de trabalho remota na VM de destino Olá: porta TCP privada de saudação do ponto de extremidade de saudação deve corresponder em qual Olá serviços de área de trabalho remota da VM está escutando a porta TCP hello (o padrão é 3389).
* Olá ACL para ponto de extremidade do tráfego de área de trabalho remota de Olá na VM de destino Olá: ACLs permitem toospecify permitido ou negado o tráfego de entrada da saudação baseado na Internet em seu endereço IP de origem. As ACLs configuradas incorretamente podem impedir que o ponto de extremidade toohello tráfego de entrada área de trabalho remota. Verifique seu tooensure ACLs que o tráfego de entrada de seus endereços IP públicos do seu proxy ou outro servidor de borda é permitido. Para obter mais informações, veja [O que é uma ACL (Lista de Controle de Acesso) de Rede?](../../virtual-network/virtual-networks-acl.md)

toocheck se o ponto de extremidade de saudação for origem Olá Olá problema, remova o ponto de extremidade atual hello e criar um novo, escolha uma porta aleatória na 49152-65535 Olá intervalo para o número da porta externa hello. Para obter mais informações, consulte [como tooset máquina de virtual pontos de extremidade tooa](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Fonte 4: Grupos de segurança de rede
Os grupos de segurança de rede proporcionam um controle mais granular do tráfego de entrada e de saída permitido. Você pode criar regras que abrangem sub-redes e serviços de nuvem em uma rede virtual do Azure.

Use [Verifique se o fluxo IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm se uma regra em um grupo de segurança de rede está bloqueando o tráfego tooor de uma máquina virtual. Você também pode analisar as regras de entrada tooensure "Permitir" NSG regra existe e é priorizada para a porta do RDP (padrão 3389) do grupo de segurança efetiva. Para obter mais informações, consulte [fluxo de tráfego usando regras de segurança efetiva tootroubleshoot VM](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Fonte 5: VM do Azure Baseada em Windows
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Siga as instruções de saudação em [neste artigo](reset-rdp.md). Este artigo redefine o serviço de área de trabalho remota Olá na máquina virtual de saudação:

* Habilite a regra padrão do Firewall do Windows "Área de trabalho remota" hello (porta TCP 3389).
* Habilite conexões de área de trabalho remota, definindo Olá HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections registro valor too0.

Tente a conexão de saudação do seu computador novamente. Se você ainda não é possível tooconnect via área de trabalho remota, verifique Olá problemas possíveis a seguir:

* Olá serviços de área de trabalho remota não está em execução na VM de destino hello.
* Olá serviços de área de trabalho remota não está escutando na porta TCP 3389.
* O Firewall do Windows ou outro firewall local tem uma regra de saída que está impedindo o tráfego de Área de Trabalho Remota.
* Detecção de intrusão ou software em execução na máquina virtual do Azure de saudação de monitoramento de rede está impedindo conexões de área de trabalho remota.

Para VMs criadas usando o modelo de implantação clássico hello, você pode usar um toohello de sessão remota do PowerShell do Azure máquina virtual do Azure. Primeiro, é necessário tooinstall um certificado para o serviço de nuvem de hospedagem de saudação máquina virtual. Vá muito[tooAzure de configurar o acesso remoto seguro PowerShell máquinas virtuais](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) e baixar Olá **InstallWinRMCertAzureVM.ps1** computador local de tooyour de arquivo de script.

Em seguida, instale o Azure PowerShell, se ainda não tiver feito isso. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Em seguida, abra um prompt de comando do PowerShell do Azure e alterar Olá atual toohello local da pasta Olá **InstallWinRMCertAzureVM.ps1** arquivo de script. toorun um script do PowerShell do Azure, você deve definir a política de execução correta de saudação. Executar Olá **Get-ExecutionPolicy** comando toodetermine seu nível de política atual. Para obter informações sobre como definir o nível apropriado de hello, consulte [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Em seguida, preencha a nome da sua assinatura do Azure, o nome de serviço de nuvem hello e o nome da máquina virtual (removendo hello < e > caracteres) e, em seguida, execute estes comandos.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Você pode obter o nome de assinatura correta de saudação do hello *SubscriptionName* propriedade da exibição de saudação do hello **Get-AzureSubscription** comando. Você pode obter o nome do serviço de nuvem Olá para a máquina virtual de saudação do hello *ServiceName* coluna na exibição de saudação do hello **Get-AzureVM** comando.

Verifique se você tem o novo certificado de saudação. Abrir um snap-in de certificados para o usuário atual hello e examinar Olá **\ certificados de certificação raiz confiáveis** pasta. Você deve ver um certificado com o nome DNS de saudação do seu serviço de nuvem no hello emitido toocolumn (exemplo: cloudservice4testing.cloudapp.net).

Em seguida, inicie uma sessão remota do Azure PowerShell usando estes comandos.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Depois de inserir as credenciais de administrador válida, você verá algo semelhante toohello prompt do Azure PowerShell a seguir:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Olá primeira parte desse prompt é o nome do serviço de nuvem que contém o destino Olá VM, que pode ser diferente de "cloudservice4testing.cloudapp.net". Você pode emitir comandos do PowerShell do Azure para esta nuvem mencionados de problemas do serviço tooinvestigate hello e corrigir a configuração de saudação.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually corrigir Olá Remote Desktop Services escutando a porta TCP
No prompt de sessão do PowerShell do Azure remoto hello, execute este comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Olá propriedade PortNumber mostra o número da porta atual hello. Se necessário, altere Olá área de trabalho remota porta número tooits back valor padrão (3389) usando este comando.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Verifique se que a porta de saudação foi alterado too3389 usando este comando.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Sair da sessão remota do PowerShell do Azure de saudação usando este comando.

```powershell
Exit-PSSession
```

Verifique se que esse ponto de extremidade de área de trabalho remota para hello Azure VM Olá também está usando a porta TCP 3398 como sua porta interna. Reinicie Olá VM do Azure e tente a conexão de área de trabalho remota Olá novamente.

## <a name="additional-resources"></a>Recursos adicionais
[Como tooreset uma senha ou hello área de trabalho remota de serviço para máquinas virtuais do Windows](reset-rdp.md)

[Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)

[Solucionar problemas de Secure Shell (SSH) conexões tooa baseados em Linux máquina virtual do Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Solucionar problemas de acesso tooan aplicativo em execução em uma máquina virtual do Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

