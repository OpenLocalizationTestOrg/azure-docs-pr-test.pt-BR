---
title: "políticas de laboratório básico aaaManage no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooset algumas das políticas básica de saudação (configurações) para um laboratório DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Gerenciar políticas básicas para um laboratório no Azure DevTest Labs

Azure DevTest Labs permite toocontrol custo e minimizar os desperdícios em seus laboratórios Gerenciando políticas (configurações) para cada laboratório. Neste artigo, você Introdução às políticas aprendendo como tooset duas políticas mais críticas do hello - limitando Olá número de máquinas virtuais (VM) que pode ser criadas ou solicitadas por um único usuário e desligamento automáticos configuração. tooview como tooset cada política de laboratório, consulte o artigo hello, [definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Acessar as políticas de laboratório no Azure DevTest Labs
Olá etapas a seguir orientam você durante a configuração de políticas para um laboratório no Azure DevTest Labs:

as políticas de Olá tooview (e alterar) para um ambiente de laboratório, siga estas etapas:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

1. Saudação de laboratórios, selecione lista laboratório desejado hello.   

1. Selecione **Configuração e políticas**.

    ![Folha de configurações de política](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Olá **políticas e configurações** folha contém um menu de configurações que você pode especificar. Este artigo aborda apenas as configurações de saudação de **máquinas virtuais por usuário** e **desligamento automático**. toolearn sobre Olá restantes configurações, consulte [gerenciar todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Conjunto de máquinas virtuais por usuário
Olá política para **máquinas virtuais por usuário** permite a você toospecify Olá alto número de máquinas virtuais que podem ser criados por um usuário individual. Se um usuário tentar toocreate ou declaração de uma máquina virtual quando o limite de saudação do usuário foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criado/exigida. 

1. No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por usuário**.
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selecione **Sim** toolimit Olá diversas VMs por usuário. Se você não quiser toolimit Olá diversas VMs por usuário, selecione **não**. Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário. 

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

## <a name="next-steps"></a>Próximas etapas

- [Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md) -Saiba como toomodify outras políticas de laboratório 
