---
title: toofail aaaHow do tooVMware do Azure | Microsoft Docs
description: "Após o failover de máquinas virtuais tooAzure, você pode iniciar um failback toobring máquinas virtuais back tooon local. Conhecer as etapas de saudação para como toofail fazer."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Falha do Azure tooan site local

Este artigo descreve como toofail fazer máquinas virtuais de máquinas virtuais do Azure toohello no site local. Siga as instruções de saudação em toofail este artigo fazer suas máquinas virtuais VMware ou servidores físicos do Windows/Linux depois que tiver falha de saudação local site tooAzure usando Olá [máquinas virtuais VMware replicar e física tooAzure de servidores com o Azure Site Recovery](site-recovery-vmware-to-azure-classic.md) tutorial.

> [!WARNING]
> Se você tiver [concluir a migração](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), o recurso de tooanother de máquina virtual movida Olá grupo ou excluído Olá máquina virtual do Azure, não é possível failback depois disso.

> [!NOTE]
> Se você fazer failover em máquinas virtuais VMware, em seguida, você não poderá failback tooa Hyper-v host.

## <a name="overview-of-failback"></a>Visão geral do failback
Veja como o failback funciona. Depois de fazer failover em tooAzure, você não tooyour back local em alguns estágios:

1. [Proteja](site-recovery-how-to-reprotect.md) Olá máquinas virtuais no Azure para que eles são iniciados tooreplicate tooVMware virtual máquinas no site local. Como parte desse processo, você também precisa:
    1. Configurar um destino mestre local: destino mestre do Windows para máquinas virtuais Windows e [destino mestre Linux](site-recovery-how-to-install-linux-master-target.md) para máquinas virtuais Linux.
    2. Configure um [servidor de processo](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Inicie o [proteger novamente](site-recovery-how-to-reprotect.md). Isso será desligar a máquina virtual no local, Olá e sincronizar hello Azure dados da máquina virtual com hello discos locais.
5. Depois que as máquinas virtuais no Azure estiver replicando tooyour no site local, você inicia uma falha de toohello do Azure no site local.

Depois que seus dados não novamente, você proteja Olá em máquinas virtuais que falharam, para que eles são iniciados tooreplicate tooAzure.

Para obter uma visão rápida, assista a saudação vídeo sobre como toofail através de tooan do Azure no site local a seguir.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Falha do local original ou alternativo de toohello back

Se o failover de uma máquina virtual VMware, você pode fazer back toohello mesmo local na máquina virtual de origem se ele ainda existe. Nesse cenário, somente as alterações de saudação são replicadas novamente. Esse cenário é conhecido como recuperação no local original. Se a máquina virtual no local, Olá não existir, o cenário de saudação é uma recuperação em local alternativo.

> [!NOTE]
> Você pode apenas o failback toohello original vCenter e o servidor de configuração. É possível implantar um novo servidor de configuração e usá-lo em failback. Além disso, não é possível adicionar um novo vCenter toohello existente servidor de configuração e o failback no vCenter novo hello.

#### <a name="original-location-recovery"></a>Recuperação no local original

Se você não a máquina virtual original de toohello voltar, Olá condições a seguir é necessária:
* Se a máquina virtual de saudação é gerenciada por um servidor do vCenter, em seguida, hello host do ESX do destino mestre deve ter repositório de dados do access toohello máquina virtual.
* Se Olá virtual está em um host ESX, mas não é gerenciado pelo vCenter, Olá disco da máquina virtual de saudação deve ser em um repositório de dados host de destino mestre Olá pode acessar.
* Se sua máquina virtual estiver em um host ESX e não usa o vCenter, você deve concluir a descoberta de host do ESX saudação do destino mestre Olá antes de você proteger novamente. Isso se aplicará se você também estiver realizando o failback de servidores físicos.
* Você pode fazer back tooa rede de área de armazenamento virtual (vSAN) ou um disco com base no mapeamento (RDM) se Olá discos já existem e máquina virtual local, toohello conectado de dispositivo bruto.

#### <a name="alternate-location-recovery"></a>Recuperação em local alternativo
Se a máquina virtual local, Olá não existe antes de proteger novamente a máquina virtual de Olá, o cenário de saudação é chamado uma recuperação em local alternativo. fluxo de trabalho de nova proteção Olá cria a máquina virtual no local, Olá novamente. Isso também fará um download de dados completo.

* Quando houver falha local alternativo tooan voltar, máquina virtual de saudação será recuperado toohello mesmo host ESX em qual Olá servidor de destino mestre está implantado. Olá repositório de dados que tenha usado o disco de saudação toocreate será Olá mesmo repositório de dados que foi selecionado ao proteger novamente a máquina virtual de saudação.
* Você pode fazer volta apenas tooa máquina virtual arquivo system (VMFS) repositório de dados. Se você tiver uma vSAN ou RDM, o proteger novamente e o Failback não funcionarão.
* Nova proteção envolve uma transferência de dados inicial grande seguido por alterações de saudação. Esse processo existe porque a máquina virtual de saudação não existe no local. precisam de dados completos Olá toobe replicada de volta. O proteger novamente levará mais tempo do que em uma recuperação no local original.
* Não é possível reprovar volta toovSAN RDM baseada ou discos. Somente novos discos de máquina virtual (VMDKs) podem ser criados em um datastore VMFS.

Um computador físico, quando o failover tooAzure, pode ser feito apenas como uma máquina virtual do VMware (também chamado tooas P2A2V). Esse fluxo de recuperação em local alternativo Olá se enquadra.

* Um servidor físico do Windows Server 2008 R2 SP1, se protegido e failover tooAzure, não pode ser feito novamente.
* Certifique-se de que você descobrir que pelo menos um destino mestre server e hello necessário ESX/ESXi hosts toowhich necessário toofail novamente.

## <a name="have-you-completed-reprotection"></a>Você concluiu o proteger novamente?
Antes de prosseguir, Olá completo proteja novamente as etapas para que as máquinas virtuais de saudação estão em um estado replicado, e você pode iniciar um failover tooan Voltar no site local. Para obter mais informações, consulte [como tooreprotect do Azure local tooon](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Pré-requisitos

* O servidor de configuração é necessário localmente para fazer um failback. Durante o failback, máquina virtual de saudação deve existir no banco de dados de servidor de configuração hello ou failback não tenha êxito. Sendo assim, faça o backup agendado regular de seu servidor. Se houver um desastre, você precisará toorestore servidor Olá Olá mesmo endereço IP para toowork de failback.
* o servidor de destino mestre Olá não deve ter todos os instantâneos antes de disparar o failback.

## <a name="steps-toofail-back"></a>Etapas toofail novamente

> [!IMPORTANT]
> Antes de você iniciar um failback, certifique-se de que você tenha concluído a nova proteção de máquinas virtuais de saudação. máquinas virtuais de saudação deve estar em um estado protegido e sua integridade deve ser **Okey**. máquinas de virtuais Olá tooreprotect, ler [como tooreprotect](site-recovery-how-to-reprotect.md).

1. No hello itens replicados página, selecione a máquina virtual de saudação em clique duas vezes tooselect **Failover não planejado**.
2. Em **confirmar Failover**, verifique se a direção do failover hello (do Azure) e, em seguida, selecione o ponto de recuperação do hello (mais recente ou consistente de aplicativo mais recente Olá), que você deseja toouse para failover de saudação. ponto consistente de aplicativo Hello está por trás do último ponto de saudação na hora e faz com que a perda de dados.
3. Durante o failover, recuperação de Site desliga Olá máquinas virtuais do Azure. Depois de verificar que o failback foi concluído como esperado, você pode verificar Olá máquinas virtuais do Azure foi desligadas.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>ponto de recuperação toowhat podem falhar máquinas virtuais de saudação back?

Durante o failback, você tem duas opções toofail Olá backup/recuperação de máquina virtual o plano.

Se você selecionar ponto hello mais recentes processado no momento, todas as máquinas virtuais realizarão failover tootheir último ponto disponível no momento. Caso haja um grupo de replicação no plano de recuperação Olá, e em seguida, cada máquina virtual do grupo de replicação Olá irão falhar tooits independente último ponto no tempo.

Você não pode efetuar novamente uma máquina virtual até que tenha pelo menos um ponto de recuperação. Não é possível failback um plano de recuperação até que todas as suas máquinas virtuais tenham pelo menos uma recuperação de ponto.

> [!NOTE]
> Um ponto de recuperação mais recente é um ponto de recuperação consistente com falha.

Se você selecionar o ponto de recuperação consistente de aplicativo hello, um única máquina virtual failback irá recuperar tooits último ponto de recuperação consistentes com aplicativos disponíveis. No caso de saudação de um plano de recuperação com um grupo de replicação, cada grupo de replicação irá recuperar o ponto de recuperação disponíveis tooits comum.
Observe que os pontos de recuperação consistentes de aplicativo podem ser anteriores no tempo, e pode haver perda de dados.

### <a name="what-happens-toovmware-tools-post-failback"></a>O que acontece tooVMware ferramentas lançar failback?

Durante o failover tooAzure, as ferramentas do VMware Olá não podem ser executado em Olá máquina virtual do Azure. No caso de uma máquina virtual do Windows, o ASR desabilita as ferramentas do VMware Olá durante o failover. No caso de máquina virtual do Linux, o ASR desinstala as ferramentas do VMware Olá durante o failover.

Durante o failback da máquina de virtual do Windows hello, as ferramentas do VMware hello serão habilitadas novamente após o failback. Da mesma forma, para uma máquina virtual linux, as ferramentas do VMware Olá são reinstaladas na máquina Olá durante o failback.

## <a name="next-steps"></a>Próximas etapas

Após a conclusão do failback, você precisa toocommit tooensure de máquina virtual Olá recuperados máquinas virtuais no Azure são excluídos.

### <a name="commit"></a>Confirmar
Confirmação é necessário tooremove Olá failover da máquina virtual do Azure.
Clique no item Olá protegido e clique **confirmar**. Um trabalho removerá Olá failover de máquinas virtuais no Azure.

### <a name="reprotect-from-on-premises-tooazure"></a>Proteja de tooAzure local

Após a conclusão da confirmação, sua máquina virtual está em Olá no site local, mas ele não estará protegido. toostart tooreplicate tooAzure novamente, Olá a seguir:

1. Em **cofre** > **configuração** > **replicadas itens**, selecione Olá máquinas virtuais que falharam novamente e, em seguida, clique em  **Proteger novamente**.
2. Atribua o valor de saudação saudação do servidor de processo que precisa toobe usado toosend dados back tooAzure.
3. Clique em **Okey** toobegin trabalho de nova proteção de saudação.

> [!NOTE]
> Quando uma máquina virtual no local é inicializado, levará algum tempo para agente Olá tooregister toohello back configuração server (too15 minutos). Durante esse tempo, proteja falhará e retornará uma mensagem de erro informando que o agente de saudação não está instalada. Aguarde alguns minutos e tente proteger novamente.

Depois proteja Olá trabalho é concluído, Olá virtual máquina está replicando tooAzure voltar e você pode fazer um failover.

## <a name="common-issues"></a>Problemas comuns
Certifique-se de que Olá vCenter está em um estado conectado antes de fazer um failback. Caso contrário, desconectando os discos e anexá-los back toohello máquina virtual falhará.
