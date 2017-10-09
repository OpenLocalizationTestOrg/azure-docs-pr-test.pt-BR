---
title: "políticas de laboratório aaaManage no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como os tamanhos de políticas de laboratório toodefine como VMs, VMs máximo por usuário e a automação de desligamento."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Gerenciar todas as políticas de um laboratório no Azure DevTest Labs

O Azure DevTest Labs permite controlar o custo e minimize o desperdício nos laboratórios gerenciando políticas (configurações) de cada laboratório. Este artigo explica detalhadamente como tooset cada política.  

## <a name="set-allowed-virtual-machine-sizes"></a>Definir tamanhos de máquina virtual permitidos
Hello política para Olá configuração permitidos tamanhos de VM ajuda toominimize laboratório desperdiçar, permitindo que você toospecify quais tamanhos de VM são permitidos em laboratório hello. Se essa política está ativada, apenas os tamanhos de VM da lista podem ser usado toocreate VMs.

1. No laboratório de saudação **políticas e configurações** folha, selecione **permitidos tamanhos de máquinas virtuais**.
   
    ![Tamanhos de máquinas virtuais permitidos](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Selecione **na** tooenable essa política, e **Off** toodisable-lo.

1. Se você habilitar essa política, selecione um ou mais tamanhos de VM que podem ser criados no laboratório.

1. Selecione **Salvar**.

## <a name="set-virtual-machines-per-user"></a>Conjunto de máquinas virtuais por usuário
Olá política para **máquinas virtuais por usuário** permite a você toospecify Olá alto número de máquinas virtuais que podem ser criados por um usuário individual. Se um usuário tentar toocreate ou declaração de uma máquina virtual quando o limite de saudação do usuário foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criado/exigida. 

1. No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por usuário**.
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selecione **Sim** toolimit Olá diversas VMs por usuário. Se você não quiser toolimit Olá diversas VMs por usuário, selecione **não**. Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário. 

1. Selecione **Sim** toolimit diversas Olá VMs que pode usar SSD (disco de estado sólido). Se você não quiser toolimit diversas Olá VMs que pode usar o SSD, selecione **não**. Se você selecionar **Sim**, insira um valor que indica o número máximo de saudação de máquinas virtuais que podem ser criados usando SSD. 

1. Selecione **Salvar**.

## <a name="set-virtual-machines-per-lab"></a>Conjunto de máquinas virtuais por laboratório
Olá política para **máquinas virtuais por laboratório** permite que você toospecify Olá número de máquinas virtuais que podem ser criados para o laboratório atual hello. Se um usuário tentar toocreate uma VM quando o limite de laboratório Olá foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criada. 

1. No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por laboratório**.
   
    ![Máquinas virtuais por laboratório](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Selecione **Sim** toolimit Olá diversas VMs por laboratório. Se você não quiser toolimit Olá diversas VMs por laboratório, selecione **não**. Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário. 

1. Selecione **Sim** toolimit diversas Olá VMs que pode usar SSD (disco de estado sólido). Se você não quiser toolimit diversas Olá VMs que pode usar o SSD, selecione **não**. Se você selecionar **Sim**, insira um valor que indica o número máximo de saudação de máquinas virtuais que podem ser criados usando SSD. 

1. Selecione **Salvar**.

## <a name="set-auto-shutdown"></a>Definir desligamento automático
política de desligamento automático de saudação ajuda toominimize laboratório desperdiçar, permitindo que você tenha tempo de saudação toospecify que VMs deste laboratório desligadas.

1. No laboratório de saudação **políticas e configurações** folha, selecione **desligamento automático**.
   
    ![Desligamento automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Selecione **na** tooenable essa política, e **Off** toodisable-lo.

1. Se você habilitar essa política, especifique Olá tooshut de tempo (e o fuso horário) para todas as máquinas virtuais no laboratório atual hello.

1. Especifique **Sim** ou **não** para Olá opção toosend uma toohello anterior de 15 minutos de notificação especificado o tempo de desligamento automático. Se você especificar **Sim**, insira uma notificação de saudação tooreceive de ponto de extremidade do webhook URL. Para saber mais sobre os webhooks, veja [Criar um webhook ou uma função da API do Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Selecione **Salvar**.

    Por padrão, uma vez habilitada, essa diretiva se aplica a tooall VMs no laboratório atual hello. tooremove essa configuração de uma VM específica, abra da VM Olá folha e altere seu **desligamento automático** configuração 

## <a name="set-auto-start"></a>Definir início automático
política de início automático Olá permite toospecify quando Olá máquinas virtuais no laboratório atual Olá deve ser iniciado.  

1. No laboratório de saudação **políticas e configurações** folha, selecione **Auto-start**.
   
    ![Início automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Selecione **na** tooenable essa política, e **Off** toodisable-lo.

3. Se você habilitar essa política, especifique a hora de início agendada de saudação, fuso horário e Olá dias da semana Olá para qual Olá tempo se aplica. 

4. Selecione **Salvar**.

    Uma vez habilitada, essa política não é aplicada automaticamente tooany VMs no laboratório atual Olá. tooapply tooa essa configuração VM específica, folha e alteração da VM Olá abrir seu **Auto-start** configuração 

## <a name="set-expiration-date"></a>Definir a data de validade
Você pode definir uma expiração de data em que você [criar hello VM](devtest-lab-add-vm.md). Em **configurações avançadas**, escolha Olá Calendário ícone toospecify uma data na qual Olá VM será excluída automaticamente.  Por padrão, a saudação VM nunca expirará.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Depois de definido e aplicado Olá várias configurações de política VM para o laboratório, aqui estão algumas coisas tootry lado:

* [Entender os endereços IP compartilhados](devtest-lab-shared-ip.md) -explica como compartilhado IP endereços são usados no número de saudação do DevTest Labs toominimize público IP endereços tooconnect necessária tooyour do laboratório de VMs.
* [Configurar o gerenciamento de custo](devtest-lab-configure-cost-management.md) -ilustra como Olá toouse **tendência mensal de custo estimado** gráfico  
  tooview Olá estimado custo acumulado do mês atual e o custo de final de mês de Olá projetado.
* [Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace. Este artigo ilustra como toocreate um personalizado da imagem de um arquivo VHD.
* [Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) – O Azure DevTest Labs dá suporte à criação de VMs com base em imagens do Azure Marketplace. Este artigo ilustra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório.
* [Criar uma máquina virtual em um laboratório](devtest-lab-add-vm-with-artifacts.md) -ilustra como toocreate uma VM por meio de uma imagem de base (ou personalizadas ou Marketplace) e como toowork com artefatos em sua VM.

