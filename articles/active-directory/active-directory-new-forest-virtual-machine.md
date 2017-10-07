---
title: aaaInstall uma floresta do Active Directory em uma rede virtual do Azure | Microsoft Docs
description: "Um tutorial que explica como toocreate do Active Directory uma nova floresta em uma máquina virtual (VM) em uma rede Virtual do Azure."
services: active-directory, virtual-network
keywords: "máquina virtual do active directory, instalar floresta do active directory, vídeos do active directory do azure  "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Instalar uma nova floresta do Active Directory em uma rede virtual do Azure
Este tópico mostra como toocreate um Windows Server Active Directory novo ambiente em uma rede virtual do Azure em uma máquina virtual (VM) em um [rede virtual do Azure](../virtual-network/virtual-networks-overview.md). Nesse caso, Olá rede virtual do Azure não está conectado tooan rede de local.

Você também pode estar interessado nestes tópicos relacionados:

* Para obter um vídeo que mostra essas etapas, consulte [como tooinstall do Active Directory uma nova floresta em uma rede virtual do Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* Você pode opcionalmente [configurar uma VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md) e instalar uma nova floresta ou estender um tooan de floresta local na rede virtual do Azure. Para essas etapas, consulte [Instalar um controlador de domínio do Active Directory de réplica em uma rede virtual do Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Para obter diretrizes conceituais sobre como instalar os Serviços de Domínio Active Directory (AD DS) em uma rede virtual do Azure, consulte [Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagrama do cenário
Nesse cenário, os usuários externos necessário tooaccess aplicativos que são executados em servidores de domínio. Olá VMs que executam os servidores de aplicativos Olá Olá VMs que executam os controladores de domínio são instaladas e instalado em seu próprio serviço de nuvem em uma rede virtual do Azure. Elas também estão incluídas em um conjunto de disponibilidade para melhorar a tolerância a falhas.

Floresta do ![Active Directory em máquinas virtuais na Rede Virtual do Azure ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Como isso difere do local?
Não há muita diferença entre instalar um controlador de domínio no Azure em comparação com um local. principais diferenças de saudação são listadas na Olá a tabela a seguir.

| tooconfigure... | Configuração local | rede virtual do Azure |
| --- | --- | --- |
| **Endereço IP do controlador de domínio Olá** |Atribuir um endereço IP estático em Propriedades do adaptador de rede Olá |Executar tooassign de cmdlet Set-AzureStaticVNetIP Olá um endereço IP estático |
| **Resolvedor do cliente DNS** |Definir o endereço do servidor DNS alternativo e preferencial em Olá propriedades do adaptador de rede dos membros do domínio |Definir o endereço do servidor DNS em Propriedades da rede virtual Olá Olá |
| **Armazenamento de banco de dados do Active Directory** |Opcionalmente, alterar o local de armazenamento padrão de saudação de C:\ |É necessário o local de armazenamento padrão toochange de C:\ |

## <a name="create-an-azure-virtual-network"></a>Crie uma rede virtual do Azure
1. Entrar toohello portal clássico do Azure.
2. Crie uma rede virtual. Clique em **Redes** > **Criar uma rede virtual**. Use valores de Olá Olá Assistente de saudação toocomplete tabela a seguir.

   | Nesta página do assistente… | Especifique esses valores |
   | --- | --- |
   |  **Detalhes de rede virtual** |<p>Nome: digite um nome para a sua rede virtual</p><p>Região: Escolha a região mais próxima Olá</p> |
   |  **DNS e VPN** |<p>Deixe o servidor DNS em branco</p><p>Não selecione a opção de VPN</p> |
   |  **Espaços de endereço da rede virtual** |<p>Nome da sub-rede: digite um nome para a sua sub-rede</p><p>IP Inicial: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Criar o controlador de domínio VMs toorun hello e funções de servidor DNS
Repita Olá seguindo as etapas toocreate função VMs toohost Olá DC conforme necessário. Você deve implantar pelo menos dois controladores de domínio tooprovide tolerância a falhas e redundância virtual. Se hello rede virtual do Azure inclui pelo menos dois controladores de domínio que são configurados da mesma forma (ou seja, são ambos os GCs, o servidor DNS execute, e não contém nenhuma função FSMO e assim por diante), em seguida, coloque Olá VMs que executam os controladores de domínio em uma conjunto de disponibilidade para melhorar a tolerância.

Olá toocreate VMs usando o Windows PowerShell em vez da saudação da interface do usuário, consulte [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. No portal clássico do hello, clique em **novo** > **de computação** > **Máquina Virtual** > **da galeria**. Use Olá Assistente de saudação toocomplete valores a seguir. Aceite o valor de padrão de saudação para uma configuração, a menos que outro valor é sugerido ou necessário.

   | Nesta página do assistente… | Especifique esses valores |
   | --- | --- |
   |  **Escolha uma imagem** |Windows Server 2012 R2 Datacenter |
   |  **Configuração de máquina virtual** |<p>Nome da Máquina Virtual: digite um nome de rótulo único (como AzureDC1).</p><p>Novo nome de usuário: Digite o nome de saudação de um usuário. Esse usuário será um membro do grupo de administradores local Olá em Olá VM. Você precisará toosign esse nome no toohello VM para Olá primeira vez. conta interna do Hello chamada administrador não funcionará.</p><p>Nova Senha/Confirmar: digite uma senha</p> |
   |  **Configuração de máquina virtual** |<p>O serviço de nuvem: Escolha <b>criar um novo serviço de nuvem</b> para Olá primeira máquina virtual e selecione mesmo nome do serviço de nuvem quando você criar mais VMs que hospedam Olá função do controlador de domínio.</p><p>Nome DNS do Serviço de Nuvem: especifique um nome global exclusivo</p><p>Região/grupo de afinidade/rede Virtual: especifique o nome de rede virtual da saudação (como WestUSVNet).</p><p>A conta de armazenamento: Escolha <b>usar uma conta de armazenamento gerada automaticamente</b> para Olá primeira VM e, em seguida, selecione esse nome de mesma conta de armazenamento ao criar mais VMs que hospedam Olá função do controlador de domínio.</p><p>Conjunto de Disponibilidade: escolha <b>Criar um conjunto de disponibilidade</b>.</p><p>Nome do conjunto de disponibilidade: digite um nome para a disponibilidade de saudação definida quando você cria Olá primeira VM e, em seguida, selecione o mesmo nome quando você criar VMs mais.</p> |
   |  **Configuração de máquina virtual** |<p>Selecione <b>Olá instalar agente de VM</b> e quaisquer outras extensões que você precisa.</p> |
2. Anexe um disco tooeach VM que executará a função de servidor de controlador de domínio de saudação. disco adicional Olá é o banco de dados necessário toostore Olá AD, logs e SYSVOL. Especifique um tamanho de disco de saudação (por exemplo, 10 GB) e deixe Olá **preferência de Cache do Host** definido muito**nenhum**. Para obter etapas hello, consulte [como tooAttach tooa um disco de dados Máquina Virtual do Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Depois de entrar toohello VM primeiro, abra **Gerenciador do servidor** > **serviços de arquivo e armazenamento** toocreate um volume no disco com NTFS.
4. Reserve um endereço IP estático para máquinas virtuais que executarão a função de controlador de domínio de saudação. tooreserve um endereço IP estático, baixar Olá Microsoft Web Platform Installer e [instalar o Azure PowerShell](/powershell/azure/overview) e execute o cmdlet Set-AzureStaticVNetIP do hello. Por exemplo:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Para obter mais informações sobre como definir um endereço IP estático, consulte [Configurar um endereço IP interno estático para uma VM](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Instale o Windows Server Active Directory
Use Olá rotina mesmo muito[instalar o AD DS](https://technet.microsoft.com/library/jj574166.aspx) que você use local (ou seja, você pode usar saudação da interface do usuário, um arquivo de resposta ou o Windows PowerShell). É necessário tooinstall credenciais de administrador tooprovide uma nova floresta. toospecify local Olá Olá banco de dados do Active Directory, logs e SYSVOL, alterar o local de armazenamento padrão de saudação do disco Olá sistema operacional unidade toohello dados adicionais que você anexou toohello VM.

Após a conclusão da instalação de controlador de domínio de saudação, conecte toohello VM novamente e faça logon no controlador de domínio de toohello. Lembre-se as credenciais do domínio toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Redefinir o servidor DNS Olá Olá rede virtual do Azure
1. Redefina a configuração de encaminhador DNS Olá no novo servidor de DC/DNS hello.
   1. No Gerenciador do Servidor, clique em **Ferramentas** > **DNS**.
   2. Em **Gerenciador DNS**, clique o nome de saudação do servidor DNS hello e clique em **propriedades**.
   3. Em Olá **encaminhadores** guia, clique em endereço IP de saudação do encaminhador hello e clique em **editar**.  Selecione o endereço IP hello e clique em **excluir**.
   4. Clique em **Okey** editor de saudação tooclose e **Okey** novamente tooclose Olá propriedades do servidor DNS.
2. Atualize a configuração de servidor DNS Olá para rede virtual hello.
   1. Clique em **redes virtuais** > clique duas vezes em rede virtual de saudação criada > **configurar** > **servidores DNS**, digite o nome de saudação e Olá DIP de uma das Olá VMs que executa a função de servidor DC/DNS hello e clique em **salvar**.
   2. Selecione Olá VM e clique em **reiniciar** tootrigger Olá VM tooconfigure configurações do resolvedor DNS com o endereço IP de saudação do novo servidor DNS hello.

## <a name="create-vms-for-domain-members"></a>Criar VMs para membros do domínio
1. Repita Olá seguindo as etapas toocreate VMs toorun como servidores de aplicativos. Aceite o valor de padrão de saudação para uma configuração, a menos que outro valor é sugerido ou necessário.

   | Nesta página do assistente… | Especifique esses valores |
   | --- | --- |
   |  **Escolha uma imagem** |Windows Server 2012 R2 Datacenter |
   |  **Configuração de máquina virtual** |<p>Nome da Máquina Virtual: digite um nome de rótulo único (como AppServer1).</p><p>Novo nome de usuário: Digite o nome de saudação de um usuário. Esse usuário será um membro do grupo de administradores local Olá em Olá VM. Você precisará toosign esse nome no toohello VM para Olá primeira vez. conta interna do Hello chamada administrador não funcionará.</p><p>Nova Senha/Confirmar: digite uma senha</p> |
   |  **Configuração de máquina virtual** |<p>O serviço de nuvem: Escolha **criar um novo serviço de nuvem** para Olá primeira máquina virtual e selecione que mesmo nuvem nome do serviço ao criar mais VMs que irá hospedar aplicativo hello.</p><p>Nome DNS do Serviço de Nuvem: especifique um nome global exclusivo</p><p>Região/grupo de afinidade/rede Virtual: especifique o nome de rede virtual da saudação (como WestUSVNet).</p><p>A conta de armazenamento: Escolha **usar uma conta de armazenamento gerada automaticamente** para Olá primeira VM e, em seguida, selecione esse nome de mesma conta de armazenamento ao criar mais VMs que irá hospedar aplicativo hello.</p><p>Conjunto de Disponibilidade: escolha **Criar um conjunto de disponibilidade**.</p><p>Nome do conjunto de disponibilidade: digite um nome para a disponibilidade de saudação definida quando você cria Olá primeira VM e, em seguida, selecione o mesmo nome quando você criar VMs mais.</p> |
   |  **Configuração de máquina virtual** |<p>Selecione <b>Olá instalar agente de VM</b> e quaisquer outras extensões que você precisa.</p> |
2. Depois de cada VM é provisionada, entrar e associá-la toohello domínio. Em **Gerenciador de Servidores**, clique em **Servidor Local** > **WORKGROUP** > **Alterar...** e, em seguida, selecione **domínio** e o nome do tipo saudação do seu domínio local. Forneça as credenciais de um usuário de domínio e, em seguida, reinicie o ingresso no domínio Olá Olá VM toocomplete.

Olá toocreate VMs usando o Windows PowerShell em vez da saudação da interface do usuário, consulte [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Para obter mais informações sobre como usar o Windows PowerShell, consulte [Introdução aos Cmdlets do Azure](/powershell/azure/overview) e [Referência de Cmdlets do Azure](/powershell/azure/get-started-azureps).

## <a name="see-also"></a>Consulte também
* [Como tooinstall do Active Directory uma nova floresta em uma rede virtual do Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Configurar uma VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalar uma Réplica do Controlador de Domínio do Active Directory em uma rede virtual do Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS para profissionais de TI: (01) conceitos básicos de máquina virtual](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profissionais de TI: (05) Criando redes virtuais e conectividade entre instalações](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Visão geral da Rede Virtual](../virtual-network/virtual-networks-overview.md)
* [Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)
* [PowerShell do Azure](/powershell/azure/overview)
* [Referência de Cmdlets do Azure](/powershell/azure/get-started-azureps)
* [Definir o endereço IP estático da VM do Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Como tooassign IP estático tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Instalar uma nova floresta do Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Introdução tooActive Directory Domain Services (AD DS) Virtualization (nível 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
