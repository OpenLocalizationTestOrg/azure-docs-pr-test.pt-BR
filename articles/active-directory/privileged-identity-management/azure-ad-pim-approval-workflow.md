---
title: "fluxos de trabalho de aprovação de gerenciamento de identidade com privilégios de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os fluxos de trabalho de aprovação do PIM (Privileged Identity Management)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Aprovações (Visualização)

## <a name="overview"></a>Visão geral

Com aprovações para Privileged Identity Management, você pode configurar funções toorequire aprovação para ativação e escolha um ou vários usuários ou grupos de aprovadores como delegados. Continue lendo toolearn como tooconfigure funções e selecione aprovadores.

>[!NOTE]
Tenha em mente que esse recurso ainda está em desenvolvimento e você poderá encontrar bugs. Olá funcionalidade, incluindo texto e convenções de nomenclatura estão sujeitos a alterações e não devem ser considerados finais.


## <a name="key-terminology"></a>Terminologia principal

*Usuário de função qualificado* – uma função qualificado é um usuário dentro de sua organização que foi atribuído a função tooan AD do Azure como qualificados (função exige a ativação).

*Aprovador Delegado* – um aprovador delegado é um ou vários indivíduos ou grupos do Azure AD responsáveis por aprovar solicitações de ativação de função.

## <a name="scenarios"></a>Cenários

visualização privada Olá dá suporte a saudação os seguintes cenários:

**Como um PRA (Administrador de Função com Privilégios), você pode:**

-   [habilitar a aprovação para funções específicas](#enable-approval-for-specific-roles)

-   [especificar as solicitações de tooapprove de usuários e/ou grupos do aprovador](#specify-approver-users-and/or-groups-to-approve-requests)

-   [exibir o histórico de solicitações e aprovações de todas as funções com privilégios](#view-request-and-approval-history-for-all-privileged-roles)

**Como um aprovador designado, você pode:**

-   [exibir as aprovações pendentes (solicitações)](#view-pending-approvals-requests)

-   [aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [fornecer uma justificativa para minha aprovação/rejeição](#provide-justification-for-my-approval/rejection) 

**Como um Usuário de Função Qualificada, você pode:**

-   [solicitar a ativação de uma função que exige aprovação](#request-activation-of-a-role-that-requires-approval)

-   [Exibir o status Olá tooactivate sua solicitação](#view-the-status-of-your-request-to-activate)

-   [concluir a tarefa no Azure AD caso a ativação tenha sido aprovada](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Navegação

Nós atualizamos aprovações de toosupport de navegação Olá

![](media/azure-ad-pim-approval-workflow/image001.png)

página de aterrissagem Olá fornece acesso conveniente tooinformation sobre a documentação de aprovações PIM e hello novo.

![](media/azure-ad-pim-approval-workflow/image002.png)

Também adicionamos uma nova seção para todos os usuários do PIM, “Meu Histórico de Auditoria”. Aqui você pode encontrar todas as identidades do hello informações tooyour relevantes. Isso inclui todas as suas solicitações pendentes e concluídas, qualquer decisões feitas sobre solicitações de saudação resolver e todas as suas ativações de função anteriores em um local conveniente.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Habilitar a aprovação para funções específicas

tooenable aprovação para uma função específica, primeiro selecione as funções de diretório de navegação à esquerda da saudação.

![](media/azure-ad-pim-approval-workflow/image004.png)

Localizar e selecionar as configurações no hello navegação à esquerda de funções de diretório

![](media/azure-ad-pim-approval-workflow/image006.png)

Selecionar Funções com privilégios:

![](media/azure-ad-pim-approval-workflow/image009.png)

Selecione "Ativar" na saudação exigem a seção de aprovação:

![](media/azure-ad-pim-approval-workflow/image011.png)

Uma vez habilitada, folha Olá expandirá Olá tooshow detalhes a seguir:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Se você não especificar qualquer aprovadores, Olá PRA(s) se tornam saudação padrão aprovadores. PRA(s) seria necessário tooapprove ativação todas as solicitações para essa função.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Especificar as solicitações de tooapprove de usuários e/ou grupos do aprovador

aprovação de toodelegate, clique em opção de saudação muito "Selecionar aprovadores":

![](media/azure-ad-pim-approval-workflow/image015.png)

Quando a folha de aprovadores selecione Olá carrega, você pode procurar por um usuário ou grupo específico utilizando barra de pesquisa Olá Olá superior ou selecionando na lista pré-populada hello e clique em "Select" quando terminar:

![](media/azure-ad-pim-approval-workflow/image017.png)

Observação: é possível selecionar vários usuários ou grupos por vez.

Sua seleção aparecerá na lista de saudação de aprovadores selecionados, conforme mostrado abaixo:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove um aprovador, simplesmente clique Olá remover botão próximo tootheir nome.

tooadd aprovadores adicionais, o processo de repetição hello.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Exibir o histórico de solicitações e aprovações de todas as funções com privilégios

histórico de solicitação e aprovação de tooview para todas as funções privilegiadas, selecione Histórico de auditoria do painel hello:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Você pode classificar dados Olá por ação e procure "Ativação aprovado"

### <a name="view-pending-approvals-requests"></a>Exibir as aprovações pendentes (solicitações)

Como aprovador delegado, você receberá notificações por email quando uma solicitação estiver aguardando sua aprovação. tooview essas solicitações no portal do PIM hello, na guia Painel (em nova navegação de saudação) selecione hello "aprovação solicitações pendentes" em hello esquerda a barra de navegação.

![](media/azure-ad-pim-approval-workflow/image023.png)

Aqui, você verá uma lista de solicitações com aprovação pendente:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Aprovar ou rejeitar solicitações de elevação de função (única e/ou em massa)

Selecione solicitações Olá deseja tooapprove ou negar e Olá botão na barra de ação que corresponde à sua decisão:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Fornecer uma justificativa para minha aprovação/rejeição

Isso abre um novo tooapprove de folha ou negar as solicitações de vários ao mesmo tempo. Inserir uma justificativa para sua decisão, e clique em Aprovar (ou negar) na inferior de saudação ou folha hello:

![](media/azure-ad-pim-approval-workflow/image029.png)

Quando o processo de solicitação de saudação for concluído, símbolo de status Olá refletirá a decisão tomada (neste exemplo, Olá decisão é aprovar):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Solicitar a ativação de uma função que exige aprovação

Solicitando a ativação de uma função que requer aprovação pode ser iniciada de navegação de PIM antiga hello ou navegação nova hello, como um processo de saudação para função ativação permanece Olá mesmo. Basta selecione uma função na lista de saudação de funções para ativar:

![](media/azure-ad-pim-approval-workflow/image033.png)

Se uma função com privilégios exigir a Autenticação Multifator, você deverá concluir essa tarefa primeiro:

![](media/azure-ad-pim-approval-workflow/image035.png)

Depois de concluída, clique em Ativar e forneça uma justificativa (se necessário):

![](media/azure-ad-pim-approval-workflow/image037.png)

solicitante de saudação será exibida uma notificação que Olá solicitação está com aprovação pendente:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Exibir o status Olá tooactivate sua solicitação

Exibindo o status de saudação de uma solicitação pendente tooactivate deve ser acessado do novo painel de navegação. Na barra de navegação à esquerda do hello, selecione guia de "Minhas solicitações de" hello:

![](media/azure-ad-pim-approval-workflow/image041.png)

estado da solicitação da saudação padrão é muito "Pendente", mas você pode alternar toosee todos ou solicitações negadas.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Concluir a tarefa no Azure AD caso a ativação tenha sido aprovada

Após a aprovação de solicitação hello, função hello está ativa e você pode continuar com qualquer trabalho que exija a essa função.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Próximas etapas

Seu comentário é valioso toous. Sinta-se livre tooshare comentários conosco aqui!
