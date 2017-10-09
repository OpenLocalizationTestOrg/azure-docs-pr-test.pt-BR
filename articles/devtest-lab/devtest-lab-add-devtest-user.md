---
title: "aaaAdd proprietários e usuários no Azure DevTest Labs | Microsoft Docs"
description: "Adicionar usuários e proprietários no Azure DevTest Labs usando Olá portal do Azure ou o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Adicionar usuários e proprietários aos Azure DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

O acesso a Azure DevTest Labs é controlado pelo [RBAC (Controle de Acesso Baseado em Função do Azure)](../active-directory/role-based-access-control-what-is.md). Usando o RBAC, você pode separar tarefas dentro de sua equipe em *funções* onde você conceder somente a quantidade Olá de acesso necessário toousers tooperform seus trabalhos. Três dessas funções RBAC são *Proprietário*, *Usuário dos DevTest Labs* e *Colaborador*. Neste artigo, você aprenderá quais ações podem ser executadas em cada um dos três principais funções RBAC hello. A partir daí, você aprenderá como laboratório de tooa de usuários tooadd - ambos via Olá portal e por meio de um script do PowerShell, e como os usuários tooadd Olá nível de assinatura.

## <a name="actions-that-can-be-performed-in-each-role"></a>Ações que podem ser executadas em cada função
Há três funções principais às quais você pode atribuir um usuário:

* Proprietário
* Usuário do DevTest Labs
* Colaborador

Olá tabela a seguir ilustra as ações de saudação que podem ser executadas por usuários em cada uma dessas funções:

| **Ações que os usuários nesta função podem executar** | **Usuário do DevTest Labs** | **Proprietário** | **Colaborador** |
| --- | --- | --- | --- |
| **Tarefas do laboratório** | | | |
| Adicionar o laboratório de tooa de usuários |Não |Sim |Não |
| Atualizar configurações de custo |Não |Sim |Sim |
| **Tarefas de base da VM** | | | |
| Adicionar e remover imagens personalizadas |Não |Sim |Sim |
| Adicionar, atualizar e excluir fórmulas |Sim |Sim |Sim |
| Incluir imagens do Azure Marketplace na listra branca |Não |Sim |Sim |
| **Tarefas da VM** | | | |
| Criar VMs |Sim |Sim |Sim |
| Iniciar, parar e excluir VMs |Somente máquinas virtuais criadas pelo usuário Olá |Sim |Sim |
| Atualizar políticas de VM |Não |Sim |Sim |
| Adicionar/remover discos de dados de/para máquinas virtuais |Somente máquinas virtuais criadas pelo usuário Olá |Sim |Sim |
| **Tarefas de artefato** | | | |
| Adicionar e remover repositórios de artefato |Não |Sim |Sim |
| Aplicar artefatos |Sim |Sim |Sim |

> [!NOTE]
> Quando um usuário cria uma máquina virtual, esse usuário é atribuído automaticamente toohello **proprietário** função da saudação criada VM.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Adicionar um proprietário ou usuário no nível de laboratório Olá
Os proprietários e os usuários podem ser adicionados no nível de laboratório Olá via Olá portal do Azure. Isso inclui usuários externos com uma [Conta da Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.
Olá etapas a seguir orientam você por meio do processo de saudação de adição de um laboratório de tooa proprietário ou usuário no Azure DevTest Labs:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.
4. Na folha do laboratório hello, selecione **configuração**. 
5. Em Olá **configuração** folha, selecione **usuários**.
6. Em Olá **usuários** folha, selecione **+ adicionar**.
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Em Olá **selecionar uma função** folha, função desejada Olá select. Olá seção [ações que podem ser executadas em cada função](#actions-that-can-be-performed-in-each-role) listas Olá várias ações que podem ser executadas por usuários em funções de proprietário, usuário do DevTest e colaborador hello.
8. Em Olá **adicionar usuários** folha, insira o endereço de email de saudação ou nome de usuário de saudação desejado tooadd na função hello especificado. Se o usuário Olá não for encontrado, uma mensagem de erro explica problema hello. Se o usuário Olá for encontrado, esse usuário é listado e selecionado. 
9. Selecione **Selecionar**.
10. Selecione **Okey** tooclose Olá **adicionar acesso** folha.
11. Ao retornar toohello **usuários** folha, Olá usuário foi adicionado.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>Adicionar um laboratório de tooa de usuário externo usando o PowerShell
Além disso tooadding usuários Olá portal do Azure, você pode adicionar um laboratório de tooyour de usuário externo usando um script do PowerShell. Olá seguinte exemplo, basta modificar Olá parâmetro valores em Olá **toochange valores** comentário.
Você pode recuperar Olá `subscriptionId`, `labResourceGroup`, e `labName` valores na folha de laboratório Olá no hello portal do Azure.

> [!NOTE]
> script de exemplo Hello pressupõe que Olá especificado usuário foi adicionado como um toohello de convidado do Active Directory e irá falhar se não for o caso de saudação. tooadd um usuário não Olá laboratório de tooa do Active Directory, usar Olá tooassign portal do Azure Olá tooa função, conforme ilustrado na seção hello, [adicionar um proprietário ou usuário no nível de laboratório Olá](#add-an-owner-or-user-at-the-lab-level).   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Adicionar um proprietário ou usuário no nível de assinatura de saudação
Permissões do Azure são propagadas do toochild escopo pai no Azure. Portanto, os proprietários de uma assinatura do Azure que contenha laboratórios automaticamente serão proprietários desses laboratórios. Eles também possuem Olá VMs e outros recursos criados por usuários do laboratório hello e Olá serviço Azure DevTest Labs. 

Você pode adicionar laboratório de tooa proprietários adicionais por meio de folha do laboratório Olá Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). No entanto, Olá adicionada escopo do proprietário de administração é mais estreito que o escopo do proprietário da assinatura hello. Por exemplo, a saudação adicionado proprietários não têm acesso completo toosome de recursos de saudação que são criados na assinatura Olá por Olá serviço DevTest Labs. 

tooadd tooan um proprietário assinatura do Azure, siga estas etapas:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **assinaturas** da lista de saudação.
3. Selecione a assinatura de saudação desejada.
4. Selecione o ícone **Acesso** . 
   
    ![Usuários do Access](./media/devtest-lab-add-devtest-user/access-users.png)
5. Em Olá **usuários** folha, selecione **adicionar**.
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Em Olá **selecionar uma função** folha, selecione **proprietário**.
7. Em Olá **adicionar usuários** folha, insira o nome ou endereço de email de saudação do usuário Olá deseja tooadd como proprietário. Se o usuário Olá não for encontrado, você receberá uma mensagem de erro explicando o problema de saudação. Se o usuário Olá for encontrado, esse usuário será listado em Olá **usuário** caixa de texto.
8. Selecione o nome do usuário localizada de saudação.
9. Selecione **Selecionar**.
10. Selecione **Okey** tooclose Olá **adicionar acesso** folha.
11. Ao retornar toohello **usuários** folha, Olá usuário foi adicionado como um proprietário. Esse usuário é agora um proprietário de todos os laboratórios criados sob essa assinatura e, portanto, ser capaz de tooperform tarefas de proprietário. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

