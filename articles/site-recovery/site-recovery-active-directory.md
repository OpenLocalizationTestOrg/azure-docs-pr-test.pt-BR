---
title: aaaProtect do Active Directory e o DNS com o Azure Site Recovery | Microsoft Docs
description: "Este artigo descreve como tooimplement uma solução de recuperação de desastres para o Active Directory usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Proteger o Active Directory e o DNS com o Azure Site Recovery
Aplicativos corporativos, como o SharePoint, Dynamics AX e SAP dependem do Active Directory e um toofunction de infraestrutura DNS corretamente. Quando você cria uma solução de recuperação de desastres para aplicativos, é importante tooremember que você precisa tooprotect e recupere o Active Directory e DNS antes de saudação outros componentes do aplicativo, tooensure coisas funcionem corretamente quando ocorrer um desastre.

O Site Recovery é um serviço do Azure que fornece recuperação de desastre por meio da orquestração de replicação, failover e recuperação de máquinas virtuais. Recuperação de site oferece suporte a vários cenários de replicação tooconsistently proteger e perfeitamente nuvens do failover aplicativos e máquinas virtuais do tooprivate, public ou hoster.

Com a Recuperação de Site, você pode criar um plano totalmente automatizado de recuperação de desastre para o Active Directory. Quando ocorrem interrupções, você pode iniciar um failover em poucos segundos de qualquer lugar para que o Active Directory esteja em funcionamento em alguns minutos. Se você implantou o Active Directory para vários aplicativos, como o SharePoint e SAP em seu site primário, e você desejar toofail pela completa do site hello, você pode fazer failover do Active Directory usando o primeiro Site de recuperação e failover, em seguida, Olá outros aplicativos usando planos de recuperação de aplicativos específicos.

Este artigo explica como toocreate uma solução de recuperação de desastres para o Active Directory, como tooperform planejado, não planejado e failovers de teste usando um plano de recuperação de um único clique, Olá pré-requisitos e configurações com suporte.  Antes de começar, você deve estar familiarizado com o Active Directory e o Azure Site Recovery.

## <a name="replicating-domain-controller"></a>Replicando o controlador de domínio

Você precisa toosetup [replicação do Site Recovery](#enable-protection-using-site-recovery) em pelo menos uma máquina virtual que hospeda o controlador de domínio e DNS. Se você tiver [vários controladores de domínio](#environment-with-multiple-domain-controllers) em seu ambiente, além de tooreplicating Olá máquina de virtual do controlador de domínio com o Site Recovery, você também deve ter tooset até um [docontroladordedomínioadicional](#protect-active-directory-with-active-directory-replication) no site de destino da saudação (Azure ou em um datacenter local secundário). 

### <a name="single-domain-controller-environment"></a>Ambiente de controlador de domínio único
Se você tem apenas um único controlador de domínio e de alguns aplicativos e desejar toofail em todo o site Olá juntos, recomendamos usando o controlador de domínio do Site Recovery tooreplicate Olá site secundário toohello (se você estiver realizando o failover tooAzure ou tooa site secundário). Olá mesmo replicadas domínio DNS/controlador virtual máquina pode ser usada para [failover de teste](#test-failover-considerations) também.

### <a name="environment-with-multiple-domain-controllers"></a>Ambiente com vários controladores de domínio
Se você tiver muitos aplicativos e há mais de um controlador de domínio no ambiente de hello, ou se você planejar toofail em alguns aplicativos cada vez, é recomendável que, além disso tooreplicating virtual de controlador de domínio de saudação do computador com a recuperação de Site você também Configurar um [controlador de domínio adicional](#protect-active-directory-with-active-directory-replication) no site de destino da saudação (Azure ou em um datacenter local secundário). Para [failover de teste](#test-failover-considerations), use o controlador de domínio replicado pela recuperação de Site e failover, Olá outro controlador de domínio no site de destino de saudação. 


Olá seções a seguir explicam como tooenable proteção para um controlador de domínio na recuperação de Site e como tooset um controlador de domínio no Azure.

## <a name="prerequisites"></a>Pré-requisitos
* Uma implantação local do servidor DNS e do Active Directory.
* Um cofre dos Serviços do Azure Site Recovery em uma assinatura do Microsoft Azure.
* Se você estiver replicando tooAzure, execute a ferramenta de avaliação de preparação de máquina Virtual do Azure de saudação em VMs tooensure são compatíveis com VMs do Azure e serviços de recuperação de Site do Azure.

## <a name="enable-protection-using-site-recovery"></a>Habilitar a proteção com a Recuperação de Site
### <a name="protect-hello-virtual-machine"></a>Proteger a máquina virtual de saudação
Habilite proteção da máquina de virtual DNS/controlador de domínio de saudação na recuperação de Site. Defina configurações de recuperação de Site com base no tipo de máquina virtual da saudação (Hyper-V ou VMware). controlador de domínio Olá replicada usando a recuperação de Site é usado para [failover de teste](#test-failover-considerations). Verifique se que ele atende Olá requisitos a seguir:

1. controlador de domínio de saudação é um servidor de catálogo global
2. o controlador de domínio Olá deve ser o proprietário da função FSMO Olá para as funções que serão necessários durante um failover de teste (caso contrário, essas funções precisará toobe [captado](http://aka.ms/ad_seize_fsmo) após o failover de saudação)

### <a name="configure-virtual-machine-network-settings"></a>Definir configurações de rede da máquina virtual
Para a máquina de virtual DNS/controlador de domínio hello, defina configurações de rede na recuperação de Site para que máquinas virtuais de saudação rede certa toohello anexado após o failover. 

![Configurações de rede da VM](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Proteger o Active Directory com a replicação do Active Directory
### <a name="site-to-site-protection"></a>Proteção site a site
Crie um controlador de domínio no site secundário hello. Quando você promove a função de controlador de domínio do hello servidor tooa, especifique o nome de saudação do hello mesmo domínio que está sendo usado no site primário hello. Você pode usar o hello **serviços e Sites do Active Directory** snap-in do objeto tooconfigure configurações no link de site Olá toowhich Olá sites serão adicionados. Ao definir as configurações em um link de site, você pode controlar quando a replicação ocorre entre dois ou mais sites e com que frequência. Para saber mais, veja [Agendamento da replicação entre sites](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Proteção Site ao Azure
Siga as instruções de saudação muito[criar um controlador de domínio em uma rede virtual Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Quando você promove a função de controlador de domínio do hello servidor tooa, especifique Olá mesmo nome de domínio que é usado no site primário hello.

Em seguida, [reconfigurar Olá de servidor DNS para a rede virtual Olá](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), servidor DNS Olá toouse no Azure.

![Rede do Azure](./media/site-recovery-active-directory/azure-network.png)

**DNS na Rede de produção do Azure**

## <a name="test-failover-considerations"></a>considerações sobre failover de teste
O failover de teste ocorre em uma rede isolada da rede de produção para que não ocorra impactos nas cargas de trabalho de produção.

A maioria dos aplicativos também exigem a presença de saudação de um controlador de domínio e um toofunction de servidor DNS. Portanto, antes que o aplicativo hello realizar failover, um controlador de domínio precisa toobe criado no hello isolado toobe de rede usado para failover de teste. Olá toodo de maneira mais fácil trata tooreplicate uma máquina de virtual DNS/controlador de domínio com a recuperação de Site. Em seguida, execute um failover de teste da máquina de virtual do controlador de domínio de saudação antes de executar um failover de teste saudação do plano de recuperação para o aplicativo hello. Veja como fazer isso:

1. [Replicar](site-recovery-replicate-vmware-to-azure.md) Olá máquina de virtual DNS/controlador de domínio com a recuperação de Site.
1. Crie uma rede isolada. Qualquer rede virtual criada no Azure é isolada por padrão de outras redes. É recomendável que o intervalo de endereços IP Olá para essa rede é mesmo que sua rede de produção. Não habilite a conectividade site a site nessa rede.
1. Forneça um endereço IP do DNS na rede Olá criado, como endereço IP de saudação que espera Olá tooget de máquina virtual DNS. Se você estiver replicando tooAzure, em seguida, forneça endereço IP de Olá para Olá VM que é usada no failover no **IP de destino** definindo em **de computação e rede** configurações. 

    ![IP de destino](./media/site-recovery-active-directory/DNS-Target-IP.png) **IP de destino**

    ![Rede de teste do Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS na Rede de teste do Azure**

> [!TIP]
> Tentativas de recuperação de site toocreate máquinas de virtuais de teste em uma sub-rede de mesmo nome e usando Olá mesmo IP que é fornecida em **de computação e rede** configurações de máquina virtual de saudação. Se a sub-rede de mesmo nome não está disponível no hello rede virtual do Azure fornecido para failover de teste de máquina virtual de teste será criado na sub-rede primeiro Olá em ordem alfabética. Se fizer parte de Olá escolhido sub-rede IP de destino Olá, recuperação de Site tenta máquina toocreate Olá teste failover virtual usando o IP de destino de saudação. Se Olá IP de destino não é parte da saudação escolhida sub-rede, máquina de virtual de failover de teste é criada usando qualquer IP disponível em Olá escolhido sub-rede. 
>
>


1. Se você estiver replicando tooanother no site local e você estiver usando o DHCP, siga as instruções de saudação muito[a instalação do DNS e DHCP para failover de teste](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Faça um failover de teste da máquina de virtual Olá domínio controlador executado na rede isolada hello. Use mais recente disponível **consistente com aplicativo** ponto de recuperação Olá domínio controlador máquina virtual toodo saudação do failover de teste. 
1. Execute um failover de teste Olá plano de recuperação que contém máquinas virtuais de aplicativo hello. 
1. Depois que o teste for concluído, **failover de teste de limpeza** na máquina de virtual do controlador de domínio de saudação. Esta etapa exclui o controlador de domínio de saudação que foi criada para failover de teste.


### <a name="removing-reference-tooother-domain-controllers"></a>Removendo controladores de domínio de tooother de referência
Quando você estiver fazendo um failover de teste, você não colocar todos os controladores de domínio de saudação na rede de teste de saudação. referência de saudação tooremove outros controladores de domínio que existem em seu ambiente de produção, talvez seja necessário muito[executar funções FSMO Active Directory](http://aka.ms/ad_seize_fsmo) e [a limpeza de metadados](https://technet.microsoft.com/library/cc816907.aspx) de domínio ausente controladores. 



> [!IMPORTANT]
> Algumas das configurações de saudação descritas em Olá seção a seguir não são configurações de controlador de domínio saudação padrão. Se você não quiser toomake controlador de domínio essas alterações tooa produção, você pode criar um toobe dedicado de controlador de domínio usado para failover de teste de recuperação de Site e fazer essas alterações toothat.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemas devido às defesas da virtualização 

Começando com o Windows Server 2012, [defesas adicionais foram inseridas no Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Essas proteções ajudam a proteger controladores de domínio virtualizados contra reversões de USN, desde que a plataforma do hipervisor subjacente Olá dá suporte a VM-GenerationID. Azure oferece suporte a VM-GenerationID, o que significa que os controladores de domínio que executam o Windows Server 2012 ou máquinas virtuais do Azure posteriormente tem proteções adicionais hello. 


Quando Olá VM-GenerationID é redefinida, Olá invocationID do banco de dados do hello AD DS também é redefinido, Olá pool RID é descartado e SYSVOL é marcado como não autoritativo. Para obter mais informações, consulte [tooActive Introdução virtualização de serviços de domínio do diretório](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) e [virtualização segura da DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Failover tooAzure pode fazer com que a redefinição de VM-GenerationID e que é acionada proteções adicionais hello quando Olá máquina de virtual do controlador de domínio é iniciado no Azure. Isso pode resultar em uma **um atraso significativo** sendo máquina de virtual do controlador de domínio de toohello toologin capaz de usuário. Uma vez que esse controlador de domínio seria usado apenas um failover de teste, as defesas da virtualização não são necessárias. tooensure que VM-GenerationID da máquina de virtual de controlador de domínio Olá não são alterados, em seguida, você pode alterar o valor de saudação do seguinte too4 DWORD no controlador de domínio local Olá.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Sintomas das defesas da virtualização
 
Se as defesas da virtualização entrarem em ação após um failover de teste, você poderá ver um ou mais dos seguintes sintomas:  

Alteração da ID de geração

![Alteração da ID de Geração](./media/site-recovery-active-directory/Event2170.png)

Alteração da ID de invocação

![Alteração da ID de Invocação](./media/site-recovery-active-directory/Event1109.png)

Compartilhamentos Sysvol e Netlogon não estão disponíveis

![Compartilhamento Sysvol](./media/site-recovery-active-directory/sysvolshare.png)

![NTFRS Sysvol](./media/site-recovery-active-directory/Event13565.png)

Todos os bancos de dados DFSR são excluídos

![Exclusão do BD DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Algumas das configurações de saudação descritas em Olá seção a seguir não são configurações de controlador de domínio saudação padrão. Se você não quiser toomake controlador de domínio essas alterações tooa produção, você pode criar um toobe dedicado de controlador de domínio usado para failover de teste de recuperação de Site e fazer essas alterações toothat.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Solucionando problemas do controlador de domínio durante o failover de teste


Em um prompt de comando, execute Olá toocheck de comando a seguir se o SYSVOL e NETLOGON pastas compartilhadas:

    NET SHARE

No prompt de comando hello, execute Olá após o comando tooensure que Olá controlador de domínio está funcionando corretamente.

    dcdiag /v > dcdiag.txt

No log de saída de hello, procure seguir tooconfirm de texto que Olá controlador de domínio está funcionando bem. 

* "passou no teste Connectivity"
* "passou no teste Advertising"
* "passou no teste MachineAccount"

Se hello condições anteriores forem atendidas, é provável que esse controlador de domínio hello está funcionando bem. Caso contrário, tente as etapas a seguir.


* Faça uma restauração autoritativa saudação do controlador de domínio.
    * Embora seja [não recomendável toouse FRS replicação](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), mas se você ainda estiver usando, execute as etapas de saudação fornecidas [aqui](https://support.microsoft.com/kb/290762) toodo uma restauração autoritativa. Você pode ler mais sobre Burflags descreveu no link anterior Olá [aqui](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Se você estiver usando a replicação DFSR, siga etapas de saudação disponíveis [aqui](https://support.microsoft.com/kb/2218556) toodo uma restauração autoritativa. Você também pode usar funções do Powershell disponíveis neste [link](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) para essa finalidade. 
    
* Ignorar a necessidade de sincronização inicial, definindo too0 chave do registro no controlador de domínio local Olá a seguir. Se esse DWORD não existir, você poderá criá-lo no nó 'Parameters'. Saiba mais sobre isso [aqui](https://support.microsoft.com/kb/2001093)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Desabilite o requisito de saudação que um servidor de catálogo global está disponível toovalidate logon de usuário, definindo a too1 de chave do registro no controlador de domínio local Olá a seguir. Se esse DWORD não existir, você poderá criá-lo no nó 'Lsa'. Saiba mais sobre isso [aqui](http://support.microsoft.com/kb/241789)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS e controlador de domínio em computadores diferentes
Se o DNS não está em Olá mesma máquina virtual como controlador de domínio hello, você precisa toocreate uma VM do DNS para failover de teste de saudação. Se estiver na Olá mesma VM, você poderá ignorar esta seção.

Você pode usar um servidor DNS atualizado e criar todas as zonas Olá necessário. Por exemplo, se seu domínio do Active Directory for contoso.com, você pode criar uma zona DNS com hello nome contoso.com. entradas de saudação correspondentes tooActive diretório devem ser atualizadas no DNS, da seguinte maneira:

1. Certifique-se de que essas configurações estão em vigor antes de qualquer outra máquina virtual no plano de recuperação de saudação é exibida:
   
   * zona de saudação deve ser nomeada com o nome raiz da floresta hello.
   * zona de saudação deve ser baseado em arquivo.
   * zona de saudação deve ser habilitada para atualizações seguras e não seguras.
   * resolvedor de saudação do hello máquina de virtual do controlador de domínio deve apontar toohello endereço IP da máquina de virtual Olá DNS.
2. Execute Olá comando a seguir na máquina de virtual do controlador de domínio:
   
    `nltest /dsregdns`
3. Adicionar uma zona no servidor DNS hello, permitir atualizações não seguras e adicione uma entrada para ele tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Próximas etapas
Leitura [que cargas de trabalho posso proteger?](site-recovery-workload.md) toolearn mais sobre como proteger as cargas de trabalho com o Azure Site Recovery.

