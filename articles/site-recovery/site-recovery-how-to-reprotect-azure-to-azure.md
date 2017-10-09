---
title: "tooReprotect aaaHow de failover de máquinas virtuais do Azure back tooprimary região do Azure | Microsoft Docs"
description: "Após o failover de máquinas virtuais de um tooanother de região do Azure, você pode usar máquinas de saudação do Azure Site Recovery tooprotect na direção inversa. Saiba mais etapas hello como toodo uma nova proteção antes de um failover novamente."
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
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Nova proteção de failover de região de tooprimary back região do Azure



>[!NOTE]
>
> Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.


## <a name="overview"></a>Visão geral
Quando você [failover](site-recovery-failover.md) máquinas virtuais de saudação do tooanother de uma região do Azure, máquinas virtuais de saudação estão em um estado desprotegido. Se você quiser toobring-los região primária toohello, é necessário toofirst proteger máquinas virtuais de saudação e, em seguida, o failover novamente. Não há nenhuma diferença entre como realizar failover em uma direção ou outra. Da mesma forma, após habilitar a proteção de máquinas virtuais de hello, não há nenhuma diferença entre Olá nova proteção post failover ou failback de postagem.
fluxos de trabalho tooexplain Olá de nova proteção e tooavoid confusão, usaremos Olá site primário de máquinas Olá protegido como região Ásia Oriental e Olá recuperação das máquinas Olá como região Sudeste da Ásia. Durante o failover, você vai toohello Sudeste da Ásia região do failover Olá máquinas virtuais. Antes de failback, é necessário tooreprotect máquinas de virtuais de saudação do Sudeste da Ásia back tooEast Ásia. Este artigo descreve as etapas de saudação em como tooreprotect.

> [!WARNING]
> Se você tiver [concluir a migração](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), o recurso de tooanother de máquina virtual movida Olá grupo ou excluído Olá máquina virtual do Azure, não é possível failback depois disso.

Após a conclusão de nova proteção e replicação de máquinas virtuais de saudação protegida, você pode iniciar um failover em Olá máquinas virtuais toobring-los de volta região Ásia de tooEast.

Poste comentários ou perguntas no final da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Pré-requisitos
1. máquinas virtuais de saudação deve ter sido confirmadas.
2. site de destino Olá - nesse caso hello Azure Ásia Oriental região deve estar disponível e deve ser capaz de tooaccess/criar novos recursos nessa região.

## <a name="steps-tooreprotect"></a>Etapas tooreprotect

A seguir são Olá etapas tooreprotect uma máquina virtual usando os padrões de saudação.

1. Em **cofre** > **replicadas itens**, Olá VM que passou por failover e, em seguida, selecione **proteger novamente**. Você também pode clicar em Olá máquina e selecione **proteger novamente** de botões de comando hello.

![Clique com botão direito tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. Na folha de Olá, observe a direção Olá de proteção, **Sudeste da Ásia tooEast Ásia**, já está selecionado.

![Folha da nova proteção](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Saudação de revisão **conjuntos de armazenamento e a disponibilidade do grupo, rede, recursos** informações e clique em Okey. Se houver quaisquer recursos marcados (novo), eles serão criados como parte da saudação Proteja novamente.

Isso será gatilho um trabalho Proteja novamente o trabalho que fará a propagação primeiro site de destino da saudação (SEA neste caso) com dados mais recentes de saudação e depois que for concluída, replicará deltas Olá antes do failover de você fazer tooSoutheast Ásia.

### <a name="reprotect-customization"></a>Personalização da nova proteção
Se você quiser toochoose hello rede de saudação ou de conta de armazenamento de extração durante Proteja novamente, poderá fazê-lo usando Olá personalizar opção fornecida na folha de nova proteção hello.

![Opção de personalização](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Você pode personalizar Olá seguintes propriedades ele virtual da máquina de destino durante a nova proteção.

![Folha de personalização](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Propriedade |Observações  |
|---------|---------|
|Grupo de recursos de destino     | Você pode escolher o grupo de recursos toochange Olá destino no qual a máquina de virtual será criada. Como parte de saudação da nova proteção, Olá máquina de virtual de destino será excluída, portanto, você pode escolher um novo grupo de recursos sob a qual você pode criar hello VM post failover         |
|Rede virtual de destino     | Rede não pode ser alterada durante a nova proteção de saudação. Olá toochange de rede, refazer o mapeamento de rede hello.         |
|Armazenamento de destino     | Você pode alterar a conta de armazenamento Olá toowhich Olá VM será criada após failover.         |
|Armazenamento de cache     | Você pode especificar uma conta de armazenamento de cache que será usada durante a replicação. Se você ficar com hello padrões, uma nova conta de armazenamento do cache será criada, se ele ainda não existir.         |
|Conjunto de disponibilidade     |Se a máquina virtual de saudação na Ásia Oriental fizer parte de um conjunto de disponibilidade, você pode escolher uma conjunto de disponibilidade para a máquina de virtual de destino Olá no sudeste da Ásia. Padrões encontrará conjunto de disponibilidade SEA existente hello e tente toouse-la. Durante a personalização, você pode especificar um conjunto AV totalmente novo.         |


### <a name="what-happens-during-reprotect"></a>O que acontece durante a nova proteção?

Apenas como depois Olá primeiro habilite a proteção, a seguir estão os artefatos de saudação que são gerados se você usar padrões de saudação.
1. Uma conta de armazenamento do cache é criada na região da Ásia Oriental de saudação.
2. Se a conta de armazenamento de destino hello (Olá original conta de armazenamento de saudação Sudeste da Ásia VM) não existir, um novo será criado. nome de Olá é a conta de armazenamento da máquina de virtual para a Ásia Oriental Olá o sufixo "asr".
3. Se conjunto de destino AV Olá não existe e padrões de saudação detectam que ele precisa toocreate AV um novo conjunto, em seguida, ele será criado como parte da saudação Proteja o trabalho. Se você personalizou Olá proteja, conjunto de AV Olá selecionado será usado.
4.

Olá seguem lista Olá das etapas que ocorrem quando você disparar um trabalho de nova proteção. Isso está no lado de destino caso Olá Olá máquina virtual existe.

1. Olá necessário artefatos são criados como parte da nova proteção. Se já existirem, eles serão reutilizados.
2. Olá destino lado (sudeste asiático) máquina virtual é primeiro desativada, se ele estiver em execução.
3. Olá destino lado disco de máquina virtual é copiado pelo Azure Site Recovery em um contêiner como um blob de semente.
4. Olá máquina de virtual de lado de destino é excluída.
5. blob de propagação de saudação é usado pelo tooreplicate de máquina virtual para Olá atual origem lado (Ásia Oriental). Isso garante que apenas deltas sejam replicadas.
6. principais alterações Olá entre o disco de origem hello e blob de semente de saudação são sincronizadas. Isso pode levar algum tempo toocomplete.
7. Depois que proteja Olá trabalho for concluído, a replicação delta Olá começa que cria um ponto de recuperação de acordo com a política de saudação.

> [!NOTE]
> Não é possível proteger em um nível do plano de recuperação. Você só pode proteger novamente em um nível de VM.

Depois de saudação Proteja bem-sucedida, máquina virtual de saudação entrará em um estado protegido.

## <a name="next-steps"></a>Próximas etapas

Depois de máquina virtual de saudação entrou em um estado protegido, você pode iniciar um failover. Olá failover será desligar máquina virtual de saudação na região da Ásia Oriental Azure e, em seguida, criar e inicializar máquina virtual da saudação Sudeste da Ásia região. Portanto, há um pequeno tempo de inatividade para o aplicativo hello. Portanto, escolha o tempo de saudação para failover quando seu aplicativo pode tolerar um tempo de inatividade. É recomendável que você teste primeiro failover Olá máquina virtual toomake-se de que ele está chegando corretamente, antes de iniciar um failover.

-   [Etapas tooinitiate failover de teste de máquina virtual de saudação](site-recovery-test-failover-to-azure.md)

-   [Etapas tooinitiate failover da máquina virtual de saudação](site-recovery-failover.md)
