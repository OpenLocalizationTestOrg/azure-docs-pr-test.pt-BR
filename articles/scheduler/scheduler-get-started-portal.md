---
title: aaaGet iniciado com o Agendador do Azure no portal do Azure | Microsoft Docs
description: "Introdução ao Agendador do Azure no Portal do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Introdução ao Agendador do Azure no Portal do Azure
É fácil toocreate agendado trabalhos no Agendador do Azure. Neste tutorial, você aprenderá como toocreate um trabalho. Você também aprenderá sobre os recursos de monitoramento e gerenciamento do Agendador.

## <a name="create-a-job"></a>Criar um trabalho
1. Entrar muito[portal do Azure](https://portal.azure.com/).  
2. Clique em **+ novo** > tipo *Agendador* na caixa de pesquisa hello > selecione **Agendador** nos resultados > clique **criar**.
   
    ![][marketplace-create]
3. Vamos criar um trabalho que simplesmente visita http://www.microsoft.com/ com uma solicitação GET. Em Olá **trabalho do Agendador** tela, insira Olá informações a seguir:
   
   1. **Nome:** `getmicrosoft`  
   2. **Assinatura:** sua assinatura do Azure   
   3. **Coleção de Trabalhos:** selecione uma coleção de trabalhos existente ou clique em **Criar Novo** > insira um nome.
4. Em seguida, na **as configurações de ação**, definir Olá valores a seguir:
   
   1. **Tipo de ação:** ` HTTP`  
   2. **Método:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Finalmente, vamos definir uma agenda. trabalho de saudação pode ser definido como um único trabalho, mas convém escolher um agendamento de recorrência:
   
   1. **Recorrência**: `Recurring`
   2. **Iniciar**: data de hoje
   3. **Repetir a cada**: `12 Hours`
   4. **Terminar**: dois dias após a data de hoje  
      
      ![][recurrence-schedule]
6. Clique em **Criar**

## <a name="manage-and-monitor-jobs"></a>Gerenciar e monitorar trabalhos
Quando um trabalho é criado, ele aparece no painel do Azure principal de saudação. Clique em trabalho hello e uma nova janela é aberta com hello guias a seguir:

1. Propriedades  
2. Configurações de Ação  
3. Agenda  
4. Histórico
5. Usuários
   
   ![][job-overview]

### <a name="properties"></a>Propriedades
Essas propriedades somente leitura descrevem Olá gerenciamento metadados para o trabalho do Agendador hello.

   ![][job-properties]

### <a name="action-settings"></a>Configurações de Ação
Clicar em um trabalho em Olá **trabalhos** tela permite tooconfigure de trabalho. Isso lhe permite definir configurações avançadas, se você não configurá-las no hello criação rápida assistente.

Para todos os tipos de ação, você pode alterar a política de repetição hello e ação de erro de saudação.

Para tipos de ação do trabalho HTTP e HTTPS, você pode alterar Olá método tooany permitido verbo HTTP. Você também pode adicionar, excluir ou alterar cabeçalhos hello e informações de autenticação básica.

Para tipos de ação da fila de armazenamento, você pode alterar a conta de armazenamento Olá, nome da fila, token SAS e corpo.

Para tipos de ação do barramento de serviço, você pode alterar o namespace hello, o caminho da fila/tópico, configurações de autenticação, tipo de transporte, propriedades de mensagem e corpo da mensagem.

   ![][job-action-settings]

### <a name="schedule"></a>Agenda
Isso permite a você reconfigurar a agenda de saudação, se você deseja que a agenda de saudação toochange criado na Olá rápida-Assistente para criar.

Isso é uma oportunidade toobuild [agendas complexas e recorrência avançadas em seu trabalho](scheduler-advanced-complexity.md)

Você pode alterar a data de início hello e hora, agendamento de recorrência e Olá data de término e a hora (se o trabalho de saudação for recorrente).

   ![][job-schedule]

### <a name="history"></a>Histórico
Olá **histórico** guia exibe a métrica selecionada para cada execução do trabalho no sistema Olá para o trabalho selecionado hello. Essas métricas fornecem valores em tempo real sobre a integridade de saudação do seu Agendador:

1. Status  
2. Detalhes  
3. Tentativas de repetição
4. Ocorrência: 1ª, 2ª, 3ª etc.
5. Hora de início da execução  
6. Hora de término da execução
   
   ![][job-history]

Você pode clicar em uma execução tooview seu **detalhes de histórico**, incluindo a resposta inteira Olá para cada execução. Essa caixa de diálogo também permite que você toocopy Olá resposta toohello da área de transferência.

   ![][job-history-details]

### <a name="users"></a>Usuários
O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Agendador do Azure. toolearn como Olá toouse guia de usuários, consulte muito[o controle de acesso](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Agendador](scheduler-concepts-terms.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Como toobuild complexo agenda e recorrência avançadas com o Agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Agendador](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador](scheduler-high-availability-reliability.md)

 [Limites, padrões e códigos de erro do Agendador](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
