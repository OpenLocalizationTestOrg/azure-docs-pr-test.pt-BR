---
title: "aaaDisaster cenários de recuperação para máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba quais toodo no evento Olá uma interrupção de serviço do Azure afeta máquinas virtuais do Azure."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Quais toodo no evento Olá uma interrupção de serviço do Azure afeta as VMs do Azure
Na Microsoft, trabalhamos rígido toomake-se de que nossos serviços são sempre tooyou disponível quando você precisar deles. Às vezes, forças além do nosso controle nos afetam de formas que causam interrupções de serviço não planejadas.

A Microsoft fornece um SLA (Contrato de Nível de Serviço) para seus serviços como um compromisso com o tempo de atividade e a conectividade. Olá SLA para serviços do Azure individuais pode ser encontrada em [contratos de nível de serviço do Azure](https://azure.microsoft.com/support/legal/sla/).

O Azure já tem muitos recursos internos de plataforma que oferecem suporte a aplicativos altamente disponíveis. Para saber mais sobre esses serviços, leia [Recuperação de desastres e alta disponibilidade para aplicativos do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Este artigo aborda um cenário de recuperação de desastres true quando uma região inteira apresenta uma falha devido a desastres naturais toomajor ou interrupção do serviço generalizada. Eles são ocorrências raras, mas você deve preparar para a possibilidade de saudação se houver uma interrupção de uma região inteira. Se toda a região passa por uma interrupção do serviço, cópias localmente redundantes de saudação dos seus dados temporariamente seria indisponíveis. Se você tiver habilitado a replicação geográfica, haverá três cópias adicionais dos blobs de Armazenamento do Azure e tabelas armazenadas em uma região diferente. No caso de saudação de uma interrupção regional completa ou um desastre no qual Olá região primária não é recuperável, o Azure mapea novamente todas de região de replicação geográfica toohello entradas DNS hello.

toohelp tratar essas ocorrências raras, fornecemos Olá seguindo as diretrizes para máquinas virtuais do Azure no caso de saudação de uma interrupção do serviço de toda a região Olá onde seu aplicativo de máquina virtual do Azure é implantado.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Opção 1: Iniciar um failover usando o Azure Site Recovery
É possível configurar o Azure Site Recovery para suas VMs, de modo que você possa recuperar o aplicativo com um único clique em questão de minutos. Você pode replicar tooAzure região de sua escolha e regiões toopaired não restrita. Você pode começar [replicando suas máquinas virtuais](https://aka.ms/a2a-getting-started). Você pode [criar um plano de recuperação](../site-recovery/site-recovery-create-recovery-plans.md) para que você pode automatizar o processo de failover inteiro de saudação para seu aplicativo. Você pode [seu failovers de teste](../site-recovery/site-recovery-test-failover-to-azure.md) antecipadamente sem afetar produção aplicativo ou hello replicação em andamento. Em caso de saudação de uma interrupção da região primária, você apenas [iniciar um failover](../site-recovery/site-recovery-failover.md) e coloque seu aplicativo na região de destino.


## <a name="option-2-wait-for-recovery"></a>Opção 2: aguardar a recuperação
Nesse caso, nenhuma ação sua é necessária. Sabe o que estamos trabalhando cuidadosamente toorestore disponibilidade do serviço. Você pode ver o status atual do serviço Olá no nosso [painel de integridade do serviço Azure](https://azure.microsoft.com/status/).

Isso é Olá melhor opção se você não configurou o Azure Site Recovery, armazenamento com redundância geográfica com acesso de leitura ou interrupção de toohello anterior de armazenamento com redundância geográfica. Se você configurou o armazenamento com redundância geográfica ou armazenamento com redundância geográfica com acesso de leitura para a conta de armazenamento Olá onde seus discos rígidos virtuais (VHDs) de VM são armazenados, pode examinar a imagem base do toorecover Olá VHD e tente tooprovision uma nova VM dele. Essa não é uma opção preferencial, pois não há nenhuma garantia de sincronização de dados. Consequentemente, essa opção não é garantida toowork.


> [!NOTE]
> Lembre-se de que você não tem nenhum controle sobre esse processo e de que ele ocorrerá apenas em caso de interrupção do serviço em toda uma região. Por isso, você também deve contar com outra estratégias de backup específicas do aplicativo tooachieve hello mais alto nível de disponibilidade. Para obter mais informações, consulte a seção Olá em [estratégias de recuperação de desastres de dados](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Próximas etapas

- Inicie [protegendo seus aplicativos executados em máquinas virtuais do Azure](https://aka.ms/a2a-getting-started) utilizando o Azure Site Recovery

- toolearn mais sobre como tooimplement uma recuperação de desastres e estratégia de alta disponibilidade, consulte [recuperação de desastres e alta disponibilidade para aplicativos do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- toodevelop uma compreensão técnica detalhada dos recursos de uma plataforma de nuvem, consulte [orientação técnica de resiliência do Azure](../resiliency/resiliency-technical-guidance.md).


- Se instruções Olá não criptografadas, ou se você deseja que as operações de saudação do Microsoft toodo em seu nome, entre em contato com [atendimento](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
