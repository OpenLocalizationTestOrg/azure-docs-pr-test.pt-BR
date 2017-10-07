---
title: "aaaCreate conta de usuário do AD do Azure | Microsoft Docs"
description: "Este artigo descreve como as credenciais para runbooks na automação do Azure tooauthenticate no Azure e o Azure clássico toocreate uma conta de usuário do AD do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "usuário do azure active directory, gerenciamento de serviço do azure, conta de usuário do azure ad"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Autenticar Runbooks com implantação clássica do Azure e do Resource Manager
Este artigo descreve as etapas de Olá, que você deve executar tooconfigure uma conta de usuário do AD do Azure para runbooks de automação do Azure em execução no modelo de implantação clássico do Azure ou os recursos do Gerenciador de recursos do Azure.  Enquanto isso continua toobe uma identidade de autenticação com suporte para o Gerenciador de recursos do Azure com base em runbooks, Olá recomendável método é usar uma conta executar como do Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Criar um novo usuário do Azure Active Directory
1. Faça logon no portal clássico do Azure toohello como um administrador de serviço para Olá assinatura do Azure que você deseja toomanage.
2. Selecione **do Active Directory**e, em seguida, selecione o nome de saudação do diretório de sua organização.
3. Selecione Olá **usuários** guia e, em seguida, na área de comando hello, selecione **adicionar usuário**.
4. Em Olá **Conte-nos sobre este usuário** página em **tipo de usuário**, selecione **novo usuário na sua organização**.
5. Insira um nome de usuário.  
6. Selecione nome do diretório Olá que está associado à sua assinatura do Azure na página do Active Directory hello.
7. Em Olá **perfil de usuário** , forneça o primeiro e último nome, um nome amigável e usuário do hello **funções** lista.  Não selecione **Habilitar Autenticação Multifator**.
8. Observe o nome completo do usuário hello e a senha temporária.
9. Selecione **Configurações > Administradores > Adicionar**.
10. Digite o nome de usuário completo de Olá saudação do usuário de que você criou.
11. Selecione a assinatura de saudação que você deseja Olá toomanage do usuário.
12. Faça logoff do Azure e, em seguida, faça logon novamente com a conta de saudação que você acabou de criar. Você será solicitado toochange Olá a senha de usuário.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Como criar uma conta de Automação no portal clássico do Azure
Nesta seção, você deve executar Olá a seguir as etapas toocreate uma conta de automação do Azure no portal do Azure para uso de saudação com seus runbooks Gerenciando recursos de implantação clássico do Azure.  

> [!NOTE]
> Contas de automação criadas com o portal clássico do Azure Olá podem ser gerenciadas pelo Olá clássico do Azure e portal do Azure e um conjunto de cmdlets. Depois de criar conta de hello, não faz diferença como criar e gerenciar recursos na conta de saudação. Se você estiver planejando toocontinue toouse portal clássico do Azure de hello, em seguida, você deve usá-lo em vez de Olá toocreate portal do Azure as contas de automação.
> 
> 

1. Faça logon no portal clássico do Azure toohello como um administrador de serviço para Olá assinatura do Azure que você deseja toomanage.
2. Selecione **Automação**.
3. Em Olá **automação** página, selecione **criar uma conta de automação**.
4. Em Olá **criar uma conta de automação** caixa, digite um nome para sua nova conta de automação e selecione um **região** da lista suspensa de saudação.  
5. Clique em **Okey** tooaccept suas configurações e crie a conta de saudação.
6. Depois que ele é criado ele será listado em Olá **automação** página.
7. Clique na conta de saudação e ele exibirá a página painel toohello.  
8. Na página do painel de automação hello, selecione **ativos**.
9. Em Olá **ativos** página, selecione **adicionar configurações** localizado na parte inferior da saudação da página de saudação.
10. Em Olá **adicionar configurações** página, selecione **Add Credential**.
11. Em Olá **definir credenciais** página, selecione **credencial do Windows PowerShell** de saudação **tipo de credencial** suspensa lista e forneça um nome para a credencial de saudação.
12. Na seguinte Olá **definir credenciais** página, digite no nome de usuário Olá Olá AD da conta de usuário criada anteriormente Olá **nome de usuário** senha de campo e hello em hello **senha**e **Confirmar senha** campos. Clique em **Okey** toosave suas alterações.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Criar uma conta de automação em Olá portal do Azure
Nesta seção, execute Olá a seguir as etapas toocreate uma conta de automação do Azure no portal do Azure para uso de saudação com seus runbooks gerenciar recursos no modo do Azure Resource Manager.  

1. Faça logon em toohello portal do Azure como um administrador de serviço para Olá assinatura do Azure que você deseja toomanage.
2. Selecione **Contas de Automação**.
3. Na folha de contas de automação hello, clique em **adicionar**.<br><br>![Adicionar Conta de Automação](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. Em Olá **adicionar conta de automação** folha em Olá **nome** caixa, digite um nome para sua nova conta de automação.
5. Se você tiver mais de uma assinatura, especifique Olá para a nova conta de hello, bem como um novo ou existente **grupo de recursos** e um datacenter do Azure **local**.
6. Selecione o valor de saudação **Sim** para Olá **criar Azure conta executar como** opção e, em seguida, clique em Olá **criar** botão.  
   
    > [!NOTE]
    > Se você escolher toonot criar conta executar como da saudação selecionando a opção de saudação **não**, você verá uma mensagem de aviso na Olá **adicionar conta de automação** folha.  Enquanto a conta de saudação é criada e atribuída toohello **Colaborador** função na assinatura hello, ele não terá uma identidade de autenticação correspondente dentro de seu serviço de diretório de assinaturas e, portanto, nenhum acesso recursos em sua assinatura.  Isso impedirá qualquer runbooks fazendo referência a essa conta seja capaz de tooauthenticate e executar tarefas com base nos recursos do Gerenciador de recursos do Azure.
    > 
    >

    <br>![Aviso Adicionar Conta de Automação](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Enquanto o Azure cria a conta de automação hello, você pode acompanhar o progresso de saudação em **notificações** menu hello.

Quando Olá criação de credencial de saudação é concluída, é preciso toocreate Olá de tooassociate um ativo de credencial conta de automação com hello conta de usuário do AD criado anteriormente.  Lembre-se de que criamos apenas conta de automação hello e ele não está associado com uma identidade de autenticação.  Execute etapas de saudação descritas em Olá [ativos no artigo de automação do Azure de credencial](automation-credentials.md#creating-a-new-credential-asset) e insira o valor de saudação para **username** no formato de saudação **domínio \ usuário**.

## <a name="use-hello-credential-in-a-runbook"></a>Usar credencial Olá em um runbook
Você pode recuperar a credencial Olá em um runbook usando Olá [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) atividade e, em seguida, usá-lo com [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooconnect tooyour assinatura do Azure. Se credenciais Olá forem um administrador de várias assinaturas do Azure, você também deve usar [Select-AzureSubscription](http://msdn.microsoft.com/library/dn495203.aspx) toospecify Olá correto. Isso é mostrado no exemplo de saudação do Windows PowerShell abaixo que normalmente aparece na parte superior de saudação da maioria dos runbooks de automação do Azure.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Repita essas linhas após qualquer [ponto de verificação](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) em seu runbook. Se Olá runbook está suspenso e reiniciado em outro trabalho, ele precisará novamente para a autenticação de saudação tooperform.

## <a name="next-steps"></a>Próximas etapas
* Olá a revisão Olá runbook diferentes tipos e as etapas para criar seus próprios runbooks do artigo a seguir [tipos de runbook de automação do Azure](automation-runbook-types.md)

