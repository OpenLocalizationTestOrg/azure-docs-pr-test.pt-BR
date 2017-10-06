---
title: "aaaInstall um controlador de domínio do Active Directory de réplica no Azure | Microsoft Docs"
description: "Um tutorial que explica como tooinstall um controlador de domínio do Active Directory local floresta em uma máquina virtual do Azure."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Instalar uma Réplica do Controlador de Domínio do Active Directory em uma rede virtual do Azure
Este tópico mostra como tooinstall mais controladores de domínio (também conhecido como controladores de domínio de réplica) para um domínio do Active Directory local em máquinas virtuais (VMs) do Azure em uma rede virtual do Azure.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

Você também pode estar interessado nestes tópicos relacionados:

* Opcionalmente, você pode instalar uma nova floresta do Active Directory em uma rede virtual do Azure. Para essas etapas, consulte [Instalar uma nova floresta do Active Directory em uma rede virtual do Azure](active-directory-new-forest-virtual-machine.md).
* Para obter diretrizes conceituais sobre como instalar os Serviços de Domínio Active Directory (AD DS) em uma rede virtual do Azure, consulte [Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagrama do cenário
Nesse cenário, os usuários externos necessário tooaccess aplicativos que são executados em servidores de domínio. Olá VMs que executam os servidores de aplicativo hello e Olá controladores de domínio de réplica são instalados em uma rede virtual do Azure. Olá rede virtual pode ser conectado toohello local rede por um [VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md) conexão, conforme mostrado na seguinte Olá diagrama, ou você pode usar [ExpressRoute](../expressroute/expressroute-locations-providers.md) para uma conexão mais rápida.

servidores de aplicativo Hello e Olá DCs são implantados em serviços de nuvem separado toodistribute processamento de computação e do [conjuntos de disponibilidade](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para melhorar a tolerância.
Olá DCs replicam entre si e com DCs locais por meio da replicação do Active Directory. Nenhuma ferramenta de sincronização é necessária.

![Diagrama de uma réplica de controlador de domínio do Active Directory em uma rede virtual no Azure][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Criar um site do Active Directory para Olá rede virtual do Azure
É uma boa ideia toocreate um site no Active Directory que representa Olá rede região toohello rede virtual correspondente. Que ajude a otimizar a autenticação, replicação e outras operações de localização do controlador de domínio. Olá etapas a seguir explicam como toocreate um site e para obter mais informações, consulte [adicionando um novo Site](https://technet.microsoft.com/library/cc781496.aspx).

1. Abra Serviços e Sites do Active Directory: **Gerenciador do Servidor** > **Ferramentas** > **Serviços e Sites do Active Directory**.
2. Criar uma região de saudação do toorepresent de site em que você criou uma rede virtual do Azure: clique em **Sites** > **ação** > **novo site** > tipo nome de saudação do hello novo site, como Azure US West > selecione um link de site > **Okey**.
3. Criar uma sub-rede e associar o novo site de saudação: clique duas vezes em **Sites** > clique **sub-redes** > **nova sub-rede** > digite o intervalo de endereços IP de saudação do a rede virtual Hello (como 10.1.0.0/16 no diagrama do cenário Olá) > selecione Olá novo site do Azure > **Okey**.

## <a name="create-an-azure-virtual-network"></a>Crie uma rede virtual do Azure
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), clique em **novo** > **serviços de rede** > **rede Virtual**  >  **Criação personalizada** e use a seguir Olá valores toocomplete Assistente de saudação.

   | Nesta página do assistente… | Especifique esses valores |
   | --- | --- |
   |  **Detalhes de rede virtual** |<p>Nome: Digite um nome para a rede virtual hello, como WestUSVNet.</p><p>Região: Escolha a região mais próxima da saudação.</p> |
   |  **Conectividade DNS e VPN** |<p>Servidores DNS: Especifique o nome de saudação e endereço IP de um ou mais servidores DNS local.</p><p>Conectividade: selecione **Configurar uma VPN site a site**.</p><p>Rede Loca: Especifique uma nova rede local.</p><p>Se você estiver usando o ExpressRoute em vez de uma VPN, confira [Configurar uma conexão do ExpressRoute por meio de um provedor do Exchange](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Conectividade site a site** |<p>Nome: Digite um nome para a rede de local de saudação.</p><p>Endereço IP do dispositivo VPN: especifique o endereço IP público de saudação do dispositivo Olá que irão se conectar a rede virtual toohello. dispositivo VPN Olá não pode ser localizado atrás de um NAT.</p><p>Endereço: Especifica os intervalos de endereços de saudação para sua rede local (como 192.168.0.0/16 no diagrama do cenário Olá).</p> |
   |  **Espaços de endereço da rede virtual** |<p>Espaço de endereço: Especifique o intervalo de endereços IP hello para VMs que você deseja toorun em Olá rede virtual do Azure (como 10.1.0.0/16 no diagrama do cenário Olá). Este intervalo de endereços não pode sobrepor os intervalos de endereços de saudação da rede do local de saudação.</p><p>Subredes: Especifique um nome e endereço de uma sub-rede para servidores de aplicativo hello (como front-end, 10.1.1.0/24) e para Olá controladores de domínio (como back-end, 10.1.2.0/24).</p><p>Clique em **adicionar Sub-rede de gateway**.</p> |
2. Em seguida, você configurará toocreate de gateway de rede virtual Olá uma conexão de VPN site a site segura. Consulte [configurar um Gateway de rede Virtual](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) para obter instruções de saudação.
3. Crie conexão de VPN site a site Olá entre a nova rede virtual de saudação e um dispositivo VPN local. Consulte [configurar um Gateway de rede Virtual](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) para obter instruções de saudação.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Criar máquinas virtuais do Azure para Olá funções de controlador de domínio
Repita Olá seguindo as etapas toocreate função VMs toohost Olá DC conforme necessário. Você deve implantar pelo menos dois controladores de domínio tooprovide tolerância a falhas e redundância virtual. Se hello rede virtual do Azure inclui pelo menos dois controladores de domínio que são configurados da mesma forma (ou seja, são ambos os GCs, o servidor DNS execute, e não contém nenhuma função FSMO e assim por diante), em seguida, coloque Olá VMs que executam os controladores de domínio em uma conjunto de disponibilidade para melhorar a tolerância.
Olá toocreate VMs usando o Windows PowerShell em vez da saudação da interface do usuário, consulte [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), clique em **novo** > **de computação** > **Máquina Virtual**  >  **Da galeria**. Use Olá Assistente de saudação toocomplete valores a seguir. Aceite o valor de padrão de saudação para uma configuração, a menos que outro valor é sugerido ou necessário.

   | Nesta página do assistente… | Especifique esses valores |
   | --- | --- |
   |  **Escolha uma imagem** |Windows Server 2012 R2 Datacenter |
   |  **Configuração de máquina virtual** |<p>Nome da Máquina Virtual: digite um nome de rótulo único (como AzureDC1).</p><p>Novo nome de usuário: Digite o nome de saudação de um usuário. Esse usuário será um membro do grupo de administradores local Olá em Olá VM. Você precisará toosign esse nome no toohello VM para Olá primeira vez. conta interna do Hello chamada administrador não funcionará.</p><p>Nova Senha/Confirmar: digite uma senha</p> |
   |  **Configuração de máquina virtual** |<p>O serviço de nuvem: Escolha <b>criar um novo serviço de nuvem</b> para Olá primeira máquina virtual e selecione mesmo nome do serviço de nuvem quando você criar mais VMs que hospedam Olá função do controlador de domínio.</p><p>Nome DNS do Serviço de Nuvem: especifique um nome global exclusivo</p><p>Região/grupo de afinidade/rede Virtual: especifique o nome de rede virtual da saudação (como WestUSVNet).</p><p>A conta de armazenamento: Escolha <b>usar uma conta de armazenamento gerada automaticamente</b> para Olá primeira VM e, em seguida, selecione esse nome de mesma conta de armazenamento ao criar mais VMs que hospedam Olá função do controlador de domínio.</p><p>Conjunto de Disponibilidade: escolha <b>Criar um conjunto de disponibilidade</b>.</p><p>Nome do conjunto de disponibilidade: digite um nome para a disponibilidade de saudação definida quando você cria Olá primeira VM e, em seguida, selecione o mesmo nome quando você criar VMs mais.</p> |
   |  **Configuração de máquina virtual** |<p>Selecione <b>Olá instalar agente de VM</b> e quaisquer outras extensões que você precisa.</p> |
2. Anexe um disco tooeach VM que executará a função de servidor de controlador de domínio de saudação. disco adicional Olá é o banco de dados necessário toostore Olá AD, logs e SYSVOL. Especifique um tamanho de disco de saudação (por exemplo, 10 GB) e deixe Olá **preferência de Cache do Host** definido muito**nenhum**. Para obter etapas hello, consulte [como tooAttach tooa um disco de dados Máquina Virtual do Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Depois de entrar toohello VM primeiro, abra **Gerenciador do servidor** > **serviços de arquivo e armazenamento** toocreate um volume no disco com NTFS.
4. Reserve um endereço IP estático para máquinas virtuais que executarão a função de controlador de domínio de saudação. tooreserve um endereço IP estático, baixar Olá Microsoft Web Platform Installer e [instalar o Azure PowerShell](/powershell/azure/overview) e execute o cmdlet Set-AzureStaticVNetIP do hello. Por exemplo:

    'Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM

Para obter mais informações sobre como definir um endereço IP estático, consulte [Configurar um endereço IP interno estático para uma VM](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Instale o AD DS em máquinas virtuais do Azure
Entre no tooa VM e verifique se você tem conectividade entre Olá site a site VPN ou rota expressa conexão tooresources em sua rede local. Em seguida, instale o AD DS em Olá VMs do Azure. Você pode usar o mesmo processo que você use tooinstall um controlador de domínio adicional em sua rede local (interface do usuário, o Windows PowerShell ou um arquivo de resposta). Como instalar o AD DS, certifique-se de que especificar o novo volume Olá para localização de saudação do hello banco de dados do AD, logs e SYSVOL. Se você precisar de um atualizador na instalação do AD DS, consulte [Instalar os Active Directory Domain Services (nível 100)](https://technet.microsoft.com/library/hh472162.aspx) ou [Instalar um Controlador de Domínio de Réplica do Windows Server 2012 em um Domínio Existente (nível 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Reconfigure o servidor DNS para a rede virtual Olá
1. Em Olá [portal do Azure](https://portal.azure.com), em Olá **pesquisar recursos** , digite *redes virtuais*, em seguida, clique em **redes virtuais (clássico)** em resultados da pesquisa Hello. Clique Olá nome de rede virtual do hello e, em seguida, [reconfigurar Olá endereços IP de servidor DNS para sua rede virtual](../virtual-network/virtual-network-manage-network.md#dns-servers) toouse Olá os endereços IP estáticos atribuído toohello controladores de domínio de réplica em vez de endereços IP de saudação do DNS de um local servidores.
2. tooensure que todas as réplicas de saudação VMs de controlador de domínio na rede virtual Olá sejam configurados com toouse os servidores DNS na rede virtual do hello, clique em **máquinas virtuais**, clique em coluna de status de saudação para cada VM e, em seguida, clique em **reiniciar** . Aguarde até que mostre Olá VM **executando** estado antes de tentar toosign nele.

## <a name="create-vms-for-application-servers"></a>Crie VMs para servidores de aplicativos
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

## <a name="additional-resources"></a>Recursos adicionais
* [Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Como tooupload locais existentes tooAzure de controladores de domínio do Hyper-V usando o PowerShell do Azure](http://support.microsoft.com/kb/2904015)
* [Instalar uma nova floresta do Active Directory em uma rede virtual do Azure](active-directory-new-forest-virtual-machine.md)
* [Rede Virtual do Azure](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IaaS para profissionais de TI: (01) conceitos básicos de máquina virtual](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profissionais de TI: (05) Criando redes virtuais e conectividade entre instalações](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Cmdlets de gerenciamento do Azure](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
