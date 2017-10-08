---
title: "recomendações de alta disponibilidade do Advisor aaaAzure | Microsoft Docs"
description: "Use o Supervisor do Azure tooimprove alta disponibilidade das implantações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Recomendações de alta disponibilidade do Advisor

Azure Advisor ajuda você a garantir e melhorar a continuidade da saudação de seus aplicativos essenciais aos negócios. Você pode obter as recomendações de alta disponibilidade pelo Supervisor de saudação **alta disponibilidade** Olá Advisor painel.

![Botão de alta disponibilidade no painel de Supervisor Olá](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Assegurar tolerância a falhas de máquina virtual

O Advisor identifica máquinas virtuais que não fazem parte de um conjunto de disponibilidade e recomenda movê-las para um conjunto de disponibilidade. Para fornecer aplicativos de tooyour de redundância, é recomendável agrupar duas ou mais máquinas virtuais em um conjunto de disponibilidade. Essa configuração garante que, durante a um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual está disponível e atende Olá SLA de máquina virtual do Azure. Você pode escolher qualquer toocreate uma conjunto de disponibilidade para Olá máquina virtual ou tooadd Olá máquina virtual tooan conjunto de disponibilidade existente.

> [!NOTE]
> Se você escolher toocreate uma disponibilidade definida, você deve adicionar pelo menos uma máquina virtual mais nele. É recomendável que você agrupar dois ou mais máquinas virtuais em um disponibilidade definida tooensure que pelo menos uma máquina está disponível durante uma interrupção.

![Recomendação do Assistente: para redundância de máquina virtual, use conjuntos de disponibilidade](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Assegure que haja tolerância a falhas de conjunto de disponibilidade 

Advisor identifica os conjuntos de disponibilidade que contêm uma única máquina virtual e recomenda a adição de um ou mais tooit de máquinas virtuais. Para fornecer aplicativos de tooyour de redundância, é recomendável agrupar duas ou mais máquinas virtuais em um conjunto de disponibilidade. Essa configuração garante que, durante a um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual está disponível e atende Olá SLA de máquina virtual do Azure. Você pode escolher qualquer toocreate uma máquina virtual ou toouse uma máquina virtual existente e tooadd-toohello conjunto de disponibilidade.  

![Recomendação do orientador: adicionar um ou mais conjuntos de disponibilidade toothis de VMs](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Garantir tolerância a falhas de Gateway de Aplicativo
tooensure Olá continuidade dos negócios de aplicativos de missão crítica que são ativados pelos gateways de aplicativo, o Advisor identifica instâncias de gateway do aplicativo que não estão configuradas para tolerância a falhas e sugere que você pode executar as ações de correção . O Assistente identifica Gateways de Aplicativo de instância única médios ou grandes e recomenda adicionar pelo menos uma instância a mais. Ele também identifica instance único ou vários gateways pequeno aplicativo e recomenda migrar toomedium ou SKUs grandes. Advisor recomenda tooensure essas ações que suas instâncias de gateway do aplicativo são toosatisfy configurado Olá atuais requisitos de SLA para esses recursos.

![Recomendação do Assistente: implantar duas ou mais instâncias de Gateway de Aplicativo de porte médio ou grande](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Melhorar o desempenho de saudação e a confiabilidade dos discos da máquina virtual

Advisor identifica máquinas virtuais com discos padrão e recomenda a atualização toopremium discos.
 
O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho com uso intensivo de E/S. Os discos da máquina virtual que usam contas de Armazenamento Premium armazenam dados em SSDs (unidades de estado sólido). Para obter melhor desempenho para o seu aplicativo hello, é recomendável que você migre os discos de máquina virtual que exigem armazenamento de toopremium IOPS alto. 

Se os discos não exigirem IOPS alta, você poderá limitar os custos mantendo-o em Armazenamento Standard. O Armazenamento Standard armazena dados de disco da máquina virtual em HDDs (unidades de disco rígido) em vez de SSDs. Você pode escolher toomigrate os discos de toopremium de discos de máquina virtual. Os discos premium tem suporte com a maioria dos SKUs de máquina virtual. No entanto, em alguns casos, se desejar que os discos de premium toouse, talvez seja necessário tooupgrade também sua máquina virtual SKUs.

![Recomendação do orientador: melhorar a confiabilidade de Olá os discos da máquina virtual por meio da atualização toopremium discos](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Proteger seus dados de máquina virtual contra exclusão acidental
O Assistente identifica as máquinas virtuais em que o backup não está habilitado e recomenda habilitar o backup. Configurar o backup de máquina virtual garante a disponibilidade de saudação de seus dados críticos de negócios e oferece proteção contra corrupção ou exclusão acidental.

![Recomendação do Orientador de: configurar seus dados críticos de tooprotect de backup de máquina virtual](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Como acessar as recomendações de alta disponibilidade no Assistente

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. No painel esquerdo do hello, clique em **mais serviços**.

3. Em Olá serviço painel de menu em **monitoramento e gerenciamento**, clique em **Advisor Azure**.  
 Olá Advisor painel é exibido.

4. No painel do Advisor hello, clique em Olá **alta disponibilidade** guia e, em seguida, selecione assinatura Olá para o qual você deseja tooreceive recomendações.

> [!NOTE]
> tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor. Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão. Essa é uma *operação única*. Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as recomendações do Assistente, consulte:
* [Introdução tooAzure Advisor](advisor-overview.md)
* [Introdução ao Advisor](advisor-get-started.md)
* [Recomendações de custo do Advisor](advisor-performance-recommendations.md)
* [Recomendações de desempenho do Advisor](advisor-performance-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-security-recommendations.md)

