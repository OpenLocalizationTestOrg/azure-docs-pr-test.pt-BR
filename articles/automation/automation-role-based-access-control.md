---
title: "controle de acesso baseado em aaaRole na automação do Azure | Microsoft Docs"
description: "O RBAC (controle de acesso baseado em função) permite o gerenciamento de acesso aos recursos do Azure. Este artigo descreve como tooset o RBAC na automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "rbac de automação, controle de acesso baseado em função, rbac azure"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Controle de acesso com base em função na Automação do Azure
## <a name="role-based-access-control"></a>Controle de acesso baseado em função
O RBAC (controle de acesso baseado em função) permite o gerenciamento de acesso aos recursos do Azure. Usando [RBAC](../active-directory/role-based-access-control-configure.md), você pode separar as tarefas dentro de sua equipe e conceder apenas Olá quantidade de acesso toousers, grupos e aplicativos que precisam tooperform seus trabalhos. Acesso baseado em função pode ser concedido toousers usando Olá portal do Azure, as ferramentas de linha de comando do Azure ou APIs de gerenciamento do Azure.

## <a name="rbac-in-automation-accounts"></a>RBAC em Contas de Automação
Automação do Azure, o acesso é concedido, atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos no escopo da conta de automação de saudação. A seguir são Olá funções internas com suporte por uma conta de automação:  

| **Função** | **Descrição** |
|:--- |:--- |
| Proprietário |função de proprietário de saudação permite acessar os recursos tooall e ações em uma conta de automação, inclusive fornecendo acesso tooother usuários, grupos e aplicativos toomanage Olá conta de automação. |
| Colaborador |função de Colaborador Olá permite toomanage tudo, exceto a modificação de outro usuário acessar a conta de automação de tooan de permissões. |
| Leitor |função de leitor de saudação permite que você tooview todos os recursos de saudação em uma automação contam mas não é possível fazer nenhuma alteração. |
| Operador de automação |função de operador de automação de saudação permite tarefas operacionais tooperform como iniciar, parar, suspender, continuar e agendar trabalhos. Essa função é útil se você quiser tooprotect seus recursos da conta de automação como ativos de credenciais e runbooks sejam exibidas ou modificadas, mas ainda permitir que os membros de sua organização tooexecute Esses runbooks. |
| Administrador de Acesso do Usuário |função de administrador de acesso de usuário de saudação permite toomanage contas de automação de tooAzure de acesso de usuário. |

> [!NOTE]
> Você não pode conceder acesso direitos tooa específico de runbook ou runbooks, somente os recursos de toohello e as ações dentro da saudação conta de automação.  
> 
> 

Neste artigo, irá orientá-lo como tooset o RBAC na automação do Azure. Mas primeiro, vamos tomar perto examinar Olá individuais de permissões concedido toohello Colaborador, leitor, o operador de automação e o administrador de acesso do usuário para que obtemos uma boa compreensão antes de conceder a qualquer pessoa direitos toohello conta de automação.  Caso contrário, isso poderia ter consequências indesejáveis ou não intencionais.     

## <a name="contributor-role-permissions"></a>Permissões da função Colaborador
Olá tabela a seguir apresenta ações específicas de saudação que podem ser executadas pela função de Colaborador de saudação na automação.

| **Tipo de recurso** | **Ler** | **Gravar** | **Excluir** | **Outras ações** |
|:--- |:--- |:--- |:--- |:--- |
| Conta de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de certificado de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de conexão de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de Tipo de Conexão de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de credencial de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de Agendamento de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Ativo de variável de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Configuração de Estado Desejado de Automação | | | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Tipo de Recurso de Hybrid Runbook Worker |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Trabalho de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Fluxo de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Agenda de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Módulo de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |
| Runbook de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Rascunho de Runbook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Trabalho de Teste de Rascunho de Runbook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Webhook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Permissões da função Leitor
Olá tabela a seguir apresenta ações específicas de saudação que podem ser executadas por função de leitor de saudação na automação.

| **Tipo de recurso** | **Ler** | **Gravar** | **Excluir** | **Outras ações** |
|:--- |:--- |:--- |:--- |:--- |
| Administrador de assinatura clássico |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Bloqueio de gerenciamento |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Permissão |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Operações de provedor |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Atribuição de função |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Definição de função |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Permissões de função de Operador de Automação
Olá tabela a seguir apresenta ações específicas de saudação que podem ser executadas por função de operador de automação de saudação na automação.

| **Tipo de recurso** | **Ler** | **Gravar** | **Excluir** | **Outras ações** |
|:--- |:--- |:--- |:--- |:--- |
| Conta de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de certificado de automação | | | | |
| Ativo de conexão de automação | | | | |
| Ativo de Tipo de Conexão de Automação | | | | |
| Ativo de credencial de automação | | | | |
| Ativo de Agendamento de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Ativo de variável de automação | | | | |
| Configuração de Estado Desejado de Automação | | | | |
| Tipo de Recurso de Hybrid Runbook Worker | | | | |
| Trabalho de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |
| Fluxo de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Agenda de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | |
| Módulo de Automação | | | | |
| Runbook de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rascunho de Runbook de Automação | | | | |
| Trabalho de Teste de Rascunho de Runbook de Automação | | | | |
| Webhook de Automação | | | | |

Para obter mais detalhes, Olá [ações de operador de automação](../active-directory/role-based-access-built-in-roles.md#automation-operator) listas Olá ações com suporte pela função de operador de automação Olá na conta de automação hello e seus recursos.

## <a name="user-access-administrator-role-permissions"></a>Permissões da função Administrador de Acesso do Usuário
Olá tabela a seguir apresenta ações específicas de saudação que podem ser executadas pela função de administrador de acesso de usuário de saudação na automação.

| **Tipo de recurso** | **Ler** | **Gravar** | **Excluir** | **Outras ações** |
|:--- |:--- |:--- |:--- |:--- |
| Conta de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de certificado de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de conexão de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de Tipo de Conexão de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de credencial de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de Agendamento de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Ativo de variável de automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Configuração de Estado Desejado de Automação | | | | |
| Tipo de Recurso de Hybrid Runbook Worker |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Trabalho de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Fluxo de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Agenda de Trabalho de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Módulo de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Runbook de Automação do Azure |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rascunho de Runbook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Trabalho de Teste de Rascunho de Runbook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Webhook de Automação |![Status Verde](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Configurar o RBAC para sua Conta de Automação usando o Portal do Azure
1. Faça logon no toohello [Portal do Azure](https://portal.azure.com/) e abra sua conta de automação da folha de contas de automação de saudação.  
2. Clique em Olá **acesso** controle Olá canto superior direito. Isso abre o hello **usuários** folha de onde você pode adicionar novos toomanage de usuários, grupos e aplicativos de sua conta de automação e funções de exibição existentes que podem ser configuradas para Olá conta de automação.  
   
   ![Botão de acesso](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Administradores de assinatura** já existe como usuário de padrão de saudação. grupo do active directory do Hello assinatura administradores inclui Olá administrador (es) de serviço e co-administrator(s) para sua assinatura do Azure. Olá administrador de serviço é o proprietário de saudação da sua assinatura do Azure e seus recursos e serão ter função de proprietário de saudação herdadas para contas de automação Olá muito. Isso significa que o acesso de saudação é **herdadas** para **administradores e coadministradores de serviço** de uma assinatura e do **atribuído** para Olá a todos os outros usuários. Clique em **administradores de assinatura** tooview mais detalhes sobre suas permissões.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Adicionar um novo usuário e atribuir uma função
1. Na folha de usuários hello, clique em **adicionar** tooopen Olá **Adicionar folha de acesso** onde você pode adicionar um usuário, grupo ou aplicativo e atribuir uma função toothem.  
   
   ![Adicionar usuário](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Selecione uma função na lista de saudação de funções disponíveis. Podemos escolher Olá **leitor** função, mas você pode escolher qualquer Olá disponíveis funções internas que oferece suporte a uma conta de automação ou qualquer função personalizada que você tenha definido.  
   
   ![Escolher função](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Clique em **adicionar usuários** tooopen Olá **adicionar usuários** folha. Se você tiver adicionado todos os usuários, grupos ou aplicativos toomanage sua assinatura, em seguida, os usuários são listados e você pode selecionar tooadd acesso. Se não existem quaisquer usuários listados, ou se usuário Olá você está interessado em Adicionar não estiver listado, em seguida, clique em **convidar** tooopen Olá **convidar um convidado** folha, onde você pode convidar um usuário com uma conta válida da Microsoft endereço de email, como Outlook.com, OneDrive ou Xbox Live Ids. Depois que você inseriu um endereço de email de saudação do usuário hello, clique em **selecione** tooadd Olá usuário e, em seguida, clique em **Okey**. 
   
   ![Adicionar usuários](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Agora você deve ver o usuário Olá adicionado toohello **usuários** folha com hello **leitor** função atribuída.  
   
   ![Listar usuários](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Você também pode atribuir um usuário toohello função hello **funções** folha. 
4. Clique em **funções** de saudação do hello usuários folha tooopen **folha funções**. Desta folha, você pode exibir o nome de saudação da função hello, número de saudação de usuários e grupos atribuídos a função toothat.
   
    ![Atribuir função na folha de usuários](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Controle de acesso baseado em função só pode ser definido no hello nível de conta de automação e não em qualquer recurso abaixo Olá conta de automação.
   > 
   > 
   
    Você pode atribuir mais de um usuário de tooa de função, grupo ou aplicativo. Por exemplo, se adicionarmos Olá **automação operador** função juntamente com hello **função leitor** toohello usuário, em seguida, eles podem exibir todos os recursos de automação hello, bem como executar trabalhos de runbook hello. Você pode expandir Olá suspensa tooview uma lista de funções atribuídas toohello usuário.  
   
    ![Exibir várias funções](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Remover um usuário
Você pode remover a permissão de acesso de saudação para um usuário que não está gerenciando Olá conta de automação, ou que não mais funcionar para a organização de saudação. A seguir são Olá etapas tooremove um usuário: 

1. De saudação **usuários** folha, a atribuição de função hello selecione que você deseja tooremove.
2. Clique em Olá **remover** botão na folha de detalhes de atribuição de saudação.
3. Clique em **Sim** tooconfirm remoção. 
   
   ![Remover usuários](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Usuário com função atribuída
Quando uma função de usuário atribuída tooa faz logon na conta de automação de tootheir, eles agora podem ver a conta do proprietário da saudação listada na lista de saudação do **diretórios padrão**. Na saudação de tooview ordem conta de automação que eles foram adicionados, eles devem alternar diretório de padrão do proprietário do toohello diretório padrão hello.  

![Diretório padrão](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Experiência do usuário para a função de Operador de Automação
Quando um usuário, que é atribuído a modos de exibição de função de operador de automação toohello conta de automação de saudação que são atribuídos ao, eles podem apenas exibir Olá a lista de runbooks, agendas e trabalhos de runbook criado em Olá conta de automação, mas não é possível exibir a sua definição. Eles podem iniciar, interromper, suspender, continuar ou agendar o trabalho de runbook hello. usuário de saudação não terá acesso tooother recursos de automação, como configurações, grupos de trabalho híbrido ou nós de DSC.  

![Nenhum tooresourcres de acesso](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Quando o usuário Olá clica no runbook hello, hello comandos tooview Olá fonte ou editar runbook Olá não são fornecidos como função de operador de automação de saudação não permite acesso toothem.  

![Nenhum runbook tooedit de acesso](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

usuário Olá terá acesso tooview e toocreate agendamentos, mas não terá acesso tooany outro tipo de ativo.  

![Nenhum tooassets de acesso](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Este usuário não tem acesso tooview Olá webhooks associado a um runbook

![Nenhum toowebhooks de acesso](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Configurar o RBAC para sua Conta de Automação usando o Azure PowerShell
Acesso baseado em função também pode ser configurado tooan conta de automação usando os seguintes Olá [cmdlets do PowerShell do Azure](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) lista todas as funções RBAC que estão disponíveis no Azure Active Directory. Você pode usar esse comando junto com hello **nome** toolist propriedade todos Olá ações que podem ser executadas por uma função específica.  
    **Exemplo:**  
    ![Obter a definição da função](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [AzureRmRoleAssignment get](https://msdn.microsoft.com/library/mt619413.aspx) listas de atribuições de função de RBAC do Azure AD em Olá especificado escopo. Sem parâmetros, este comando retorna todas as atribuições de função hello feitas na assinatura de saudação. Saudação de uso **ExpandPrincipalGroups** atribuições de acesso do parâmetro toolist para Olá especificado de usuário, bem como grupos de Olá Olá usuário é membro.  
    **Exemplo:** toolist de comando a seguir de saudação Use todos os usuários de saudação e suas funções dentro de uma conta de automação.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Obter a atribuição da função](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, grupos e aplicativos tooa determinado escopo de acesso.  
    **Exemplo:** tooassign hello "Automação operador" função um usuário no escopo da conta de automação de saudação do comando de uso a seguir de saudação.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Nova atribuição de função](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Use [AzureRmRoleAssignment remover](https://msdn.microsoft.com/library/mt603781.aspx) tooremove acesso de um usuário, grupo ou um aplicativo de um escopo específico.  
    **Exemplo:** tooremove usuário de saudação da função de "Operador de automação" hello no escopo da conta de automação de saudação do comando de uso a seguir de saudação.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

Olá acima exemplos, substitua **entrar Id**, **Id de assinatura**, **nome do grupo de recursos** e **nome da conta de automação** com seu detalhes da conta. Escolha **Sim** quando solicitado tooconfirm antes de continuar a atribuição de função de usuário tooremove.   

## <a name="next-steps"></a>Próximas etapas
* Para obter informações sobre diferentes maneiras tooconfigure RBAC para automação do Azure, consulte muito[gerenciar RBAC com o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Para obter detalhes sobre diferentes maneiras toostart um runbook, consulte [iniciando um runbook](automation-starting-a-runbook.md)
* Para obter informações sobre os tipos de runbook diferente, consulte muito[tipos de runbook de automação do Azure](automation-runbook-types.md)

