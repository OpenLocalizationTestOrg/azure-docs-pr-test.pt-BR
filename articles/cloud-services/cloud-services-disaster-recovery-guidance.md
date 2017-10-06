---
title: "toodo aaaWhat no evento de saudação de uma interrupção de serviço do Azure que afeta os serviços de nuvem do Azure | Microsoft Docs"
description: "Saiba quais toodo no evento de saudação de uma interrupção de serviço do Azure que afeta os serviços de nuvem do Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Quais toodo no evento de saudação de uma interrupção de serviço do Azure que afeta os serviços de nuvem do Azure
Na Microsoft, trabalhamos rígido toomake-se de que nossos serviços são sempre tooyou disponível quando você precisar deles. Às vezes, forças além do nosso controle nos afetam de formas que causam interrupções de serviço não planejadas.

A Microsoft fornece um SLA (Contrato de Nível de Serviço) para seus serviços como um compromisso com o tempo de atividade e a conectividade. Olá SLA para serviços do Azure individuais pode ser encontrada em [contratos de nível de serviço do Azure](https://azure.microsoft.com/support/legal/sla/).

O Azure já tem muitos recursos internos de plataforma que oferecem suporte a aplicativos altamente disponíveis. Para saber mais sobre esses serviços, leia [Recuperação de desastres e alta disponibilidade para aplicativos do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Este artigo aborda um cenário de recuperação de desastres true quando uma região inteira apresenta uma falha devido a desastres naturais toomajor ou interrupção do serviço generalizada. Eles são ocorrências raras, mas você deve preparar para a possibilidade de saudação se houver uma interrupção de uma região inteira. Se toda a região passa por uma interrupção do serviço, cópias localmente redundantes de saudação dos seus dados temporariamente seria indisponíveis. Se você tiver habilitado a replicação geográfica, haverá três cópias adicionais dos blobs de Armazenamento do Azure e tabelas armazenadas em uma região diferente. No caso de saudação de uma interrupção regional completa ou um desastre no qual Olá região primária não é recuperável, o Azure mapea novamente todas de região de replicação geográfica toohello entradas DNS hello.

> [!NOTE]
> Lembre-se de que você não tem qualquer controle sobre esse processo e de que ele ocorrerá apenas em caso de interrupção do serviço em todo um datacenter. Por isso, você também deve contar com outra estratégias de backup específicas do aplicativo tooachieve hello mais alto nível de disponibilidade. Para saber mais, confira [Recuperação de desastres e alta disponibilidade para aplicativos criados no Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Se você quiser tooaffect capaz de toobe seu próprios failover, talvez você queira uso Olá tooconsider [armazenamento com redundância geográfica com acesso de leitura (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), que cria uma cópia somente leitura de seus dados em outra região.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Opção 1: use uma implantação de backup por meio do Gerenciador de Tráfego do Azure
solução de recuperação de desastres mais robusta Olá envolve manter várias implantações do seu aplicativo em diferentes regiões e, em seguida, usando [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect tráfego entre elas. O Azure Traffic Manager fornece vários [métodos de roteamento](../traffic-manager/traffic-manager-routing-methods.md), portanto, você pode escolher se toomanage suas implantações usando um modelo de principais de backup ou toosplit tráfego entre elas.

![Balanceamento dos Serviços de Nuvem do Azure em regiões com o Gerenciador de Tráfego do Azure](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Olá mais rápido resposta toohello perda de uma região, é importante que você configure o Gerenciador de tráfego [monitoramento de ponto de extremidade](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Opção 2: Implantar a nova região de aplicativo tooa
Manter várias implantações active conforme descrito na opção anterior Olá incorre em custos adicionais de em andamento. Se seu objetivo de tempo de recuperação (RTO) é flexível o suficiente e você tiver código original hello ou pacote de serviços de nuvem compilado, você pode criar uma nova instância do seu aplicativo em outra região e DNS registros toopoint toohello nova implantação de atualização.

Para obter mais detalhes sobre como toocreate e implantar um aplicativo de serviço de nuvem, consulte [como toocreate e implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).

Dependendo de suas fontes de dados do aplicativo, talvez seja necessário toocheck procedimentos de recuperação de saudação para sua fonte de dados do aplicativo.

* Para fontes de dados de armazenamento do Azure, consulte [replicação de armazenamento do Azure](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck nas opções de saudação que estão disponíveis com base em Olá escolheu o modelo de replicação para o seu aplicativo.
* Para fontes de banco de dados SQL, leia [visão geral: negócios continuidade e banco de dados de recuperação de desastres com banco de dados SQL na nuvem](../sql-database/sql-database-business-continuity.md) toocheck nas opções de saudação que estão disponíveis com base no modelo de replicação de saudação escolhido para seu aplicativo.


## <a name="option-3-wait-for-recovery"></a>Opção 3: aguardar a recuperação
Nesse caso, é necessária nenhuma ação de sua parte, mas o serviço ficará indisponível até que a região Olá é restaurado. Você pode ver o status atual do serviço Olá no hello [painel de integridade do serviço Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como tooimplement uma recuperação de desastres e estratégia de alta disponibilidade, consulte [recuperação de desastres e alta disponibilidade para aplicativos do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

toodevelop uma compreensão técnica detalhada dos recursos de uma plataforma de nuvem, consulte [orientação técnica de resiliência do Azure](../resiliency/resiliency-technical-guidance.md).
