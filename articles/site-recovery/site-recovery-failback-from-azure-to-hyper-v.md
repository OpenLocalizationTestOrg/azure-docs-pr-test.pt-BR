---
title: "aaaFailback no Azure Site Recovery para máquinas virtuais Hyper-v | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação hello, failover e recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre o failback de datacenter local tooon do Azure."
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
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Failback no Site Recovery para máquinas virtuais do Hyper-V

Este artigo descreve como máquinas virtuais de toofailback protegida pela recuperação de Site.

## <a name="prerequisites"></a>Pré-requisitos
1. Certifique-se de que esse servidor de Hyper-V/server Olá site primário do VMM está conectado.
2. Você deve ter sido executada **confirmar** na máquina virtual de saudação.

## <a name="why-is-there-no-button-called-failback"></a>Por que não há um botão chamado failback?
No portal de hello, não há nenhum gesto explícito chamado failback. Failback é uma etapa em que você volte site primário toohello. Por definição, o failover ocorre quando você máquinas de virtuais de saudação do failover de primary(on-premises) site toorecovery (Azure) e o failback é quando você executar failover em máquinas virtuais Olá da recuperação faz tooprimary.

Quando você iniciar um failover, folha Olá informa sobre a direção de saudação do trabalho de saudação. Se a direção de saudação for tooOn-local do Azure, é um failback.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Por que há apenas um toofailback de gesto de failover planejado?
O Azure é um ambiente altamente disponível, e as máquinas virtuais estarão sempre disponíveis. Failback é uma atividade planejada onde você decidir tootake um pequeno tempo de inatividade para que cargas de trabalho Olá podem iniciar a execução local novamente. Isso não tem expectativa de perda de dados. Portanto, se houver apenas um gesto de failover planejado, que será desativar Olá VMs no Azure, baixar alterações mais recentes hello e certifique-se de que não há nenhuma perda de dados.

## <a name="initiate-failback"></a>Iniciar o failback
Após o failover de local de toosecondary primária hello, as máquinas virtuais replicadas não estão protegidas pela recuperação de Site e local secundário Olá agora está atuando como local ativo hello. Siga estes procedimentos toofail toohello back site primário original. Este procedimento descreve como toorun um failover planejado para uma recuperação do plano. Alternativamente, você pode executar failover Olá para uma única máquina virtual em Olá **máquinas virtuais** guia.

1. Selecione **Planos de Recuperação** > *recoveryplan_name*. Clique em **Failover** > **Planned Failover**.
2. Em hello * * confirmar Failover planejado * * página, escolha os locais de origem e destino hello. Observe a direção do failover hello. Se o failover de saudação do primário trabalhou como esperado e todas as máquinas virtuais estão no local secundário hello, que isso é apenas para fins informativos.
3. Se estiver fazendo failback do Azure, selecione as configurações em **Sincronização de Dados**:

   * **Sincronizar os dados antes do failover (sincronizar apenas alterações delta)**: essa opção minimiza o tempo de inatividade das máquinas virtuais, pois elas não são desligadas durante a sincronização. Olá a seguir:
     * Fase 1: Usa o instantâneo de máquina virtual de saudação no Azure e copia host de Hyper-V toohello local. máquina de saudação continua em execução no Azure.
     * Fase 2: Desliga Olá máquina virtual do Azure para que nenhuma nova alteração ocorre existe. Olá final do conjunto de alterações delta são transferidos toohello servidor de local e a máquina virtual no local, Olá é iniciada.

    - **Sincronizar os dados apenas durante o failover (download completo)**: use essa opção se você estiver executando no Azure por um longo período. Essa opção é mais rápida porque esperamos que a maioria do disco Olá foi alterado e não queremos toospend tempo no cálculo da soma de verificação. Ele executa um download do disco de saudação. Também é útil quando a máquina de virtual Olá local foi excluída.

    >[!NOTE]
    >Recomendamos que você use esta opção se você esteve executando Azure por um tempo (um mês ou mais) ou Olá local virtual máquina foi excluída. Essa opção não executará os cálculos de soma de verificação.
    >
    >




4. Se a criptografia de dados está habilitada para nuvem Olá, em **chave de criptografia** certificado Olá selecione emitido quando você tiver habilitado a criptografia de dados durante a instalação do provedor no servidor do VMM hello.
5. Inicie o failover de saudação. Você pode acompanhar o progresso de failover de saudação em Olá **trabalhos** guia.
6. Se você tiver selecionado Olá opção toosynchronize Olá dados antes do failover hello, uma vez saudação inicial de sincronização de dados for concluída e você está pronto tooshut Olá máquinas de virtuais no Azure, clique em **trabalhos** nome do trabalho de failover planejado **Concluir o Failover**. Isso fecha Olá máquina do Azure, Olá transferências mais recentes alterações máquina virtual local, toohello e inicia Olá VM local.
7. Agora você pode fazer logon em Olá toovalidate de máquina virtual está disponível como esperado.
8. Olá VM está em um estado de confirmação pendente. Clique em **confirmar** toocommit Olá failover.
9. Agora toocomplete Olá failback clicar em **replicação inversa** toostart proteger máquina virtual de saudação no site primário hello.

## <a name="failback-tooan-alternate-location"></a>Local alternativo de tooan de failback
Se você implantou a proteção entre um [site Hyper-V e o Azure](site-recovery-hyper-v-site-to-azure.md) ter tooability toofailback do Azure tooan alternativo no local. Isso é útil se você precisar tooset o novo hardware local. Veja como fazer isso.

1. Se você estiver instalando um novo hardware instalar o Windows Server 2012 R2 e Olá a função Hyper-V no servidor de saudação.
2. Crie um comutador de rede virtual com Olá mesmo nome que você tinha no servidor original hello.
3. Selecione **itens protegidos** -> **grupo de proteção**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> desejado toofail novamente e selecione **planejado Failover**.
4. Em **Confirmar Failover Planejado** select **Criar máquina virtual local se ela não existir**.
5. Em **nome de Host** selecione Olá novo servidor de host do Hyper-V no qual você deseja tooplace Olá VM.
6. Sincronização de dados, é recomendável selecionar opção de saudação **sincronizar dados Olá antes do failover Olá**. Essa opção minimiza o tempo de inatividade das máquinas virtuais, uma vez que faz a sincronização sem desligá-las. Olá a seguir:

   * Fase 1: Usa o instantâneo de máquina virtual de saudação no Azure e copia host de Hyper-V toohello local. máquina de saudação continua em execução no Azure.
   * Fase 2: Desliga Olá máquina virtual do Azure para que nenhuma nova alteração ocorre existe. Olá final do conjunto de alterações são transferidas toohello servidor de local e a máquina virtual no local, Olá é iniciada.
7. Clique em Olá marca de seleção toobegin Olá failover (failback).
8. Depois de concluída a sincronização inicial hello e está pronto tooshut Olá máquina de virtual no Azure, clique em **trabalhos** > <planned failover job> > **concluir o Failover**. Isso desliga Olá máquina do Azure, transferências hello mais recentes alterações toohello máquina virtual local e iniciá-lo.
9. Você pode fazer logon no tooverify de máquina virtual local Olá que tudo está funcionando conforme o esperado. Em seguida, clique em **confirmar** toofinish Olá failover.
10. Clique em **replicação inversa** toostart proteção de máquina virtual local, Olá.

    > [!NOTE]
    > Se você cancelar o trabalho de failback Olá durante a etapa de sincronização de dados, Olá local VM estará em um estado corrompido. Isso ocorre porque a sincronização de dados copia dados mais recentes de saudação de discos de dados local do toohello de discos de VM do Azure, e até a conclusão da sincronização hello, dados de disco de saudação não podem estar em um estado consistente. Se Olá VM local é iniciado depois que a sincronização de dados for cancelada, ele não pode inicializar. Disparar novamente o failover toocomplete Olá a sincronização de dados.
    >
    >



## <a name="next-steps"></a>Próximas etapas

Depois de ter concluído o trabalho de failback hello, **confirmar** máquina virtual de saudação. Confirmação exclui hello máquina virtual do Azure e seus discos e prepara Olá VM toobe protegido novamente.

Depois de **confirmar**, você pode iniciar Olá *replicação inversa*. Isso iniciará a proteger a máquina de virtual de saudação do tooAzure back local. Observe que isso será apenas as alterações de replicar hello como Olá VM foi desativada no Azure e, portanto, envia diferencial altera somente.
