---
title: "aaaCreate autônomo conta de automação do Azure | Microsoft Docs"
description: "Tutorial que orienta você através do uso de criação, teste e exemplo hello principal de autenticação de segurança na automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Como criar conta autônoma de automação do Azure
Este tópico mostra como toocreate uma conta de automação da saudação portal do Azure se você quiser tooevaluate e aprenda a automação do Azure sem incluir soluções de gerenciamento adicional de saudação ou a integração com análise de logs do OMS tooprovide monitoramento avançado do trabalhos de runbook.  Você pode adicionar essas soluções de gerenciamento ou integrar análise de Log em qualquer ponto Olá futuras.  Com hello conta de automação, você estará runbooks tooauthenticate capaz de gerenciar recursos no Gerenciador de recursos do Azure ou implantação clássica do Azure.

Quando você cria uma conta de automação em Olá portal do Azure, ele cria automaticamente:

* Conta executar como, que cria uma nova entidade de serviço no Active Directory do Azure, um certificado, e atribui hello controle de acesso baseado em função de Colaborador (RBAC), que é usada toomanage recursos de Gerenciador de recursos usando o runbooks.   
* Conta de executar como clássica, carregando um certificado de gerenciamento, que é usado os recursos clássicos toomanage usando runbooks.  

Isso simplifica o processo de saudação para você e ajuda você a iniciar rapidamente compilando e implantar runbooks toosupport precisa de sua automação.  

## <a name="permissions-required-toocreate-automation-account"></a>Permissões necessárias toocreate conta de automação
toocreate ou atualização de uma conta de automação, você deve ter Olá privilégios específicos a seguir e as permissões necessárias toocomplete neste tópico.   
 
* Em ordem toocreate uma conta de automação, sua conta de usuário do AD precisa toobe tooa adicionado função com a função de proprietário de toohello equivalente de permissões para recursos do Microsoft conforme descrito no artigo [controle de acesso baseado em função na automação do Azure ](automation-role-based-access-control.md).  
* Se os registros do aplicativo hello configuração está definido muito**Sim**, usuários não administradores em seu locatário do AD do Azure podem [registrar aplicativos AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Se os registros do aplicativo hello configuração está definido muito**não**, usuário Olá executar essa ação deve ser um administrador global no AD do Azure. 

Se você não for um membro da instância do Active Directory da assinatura Olá antes que sejam adicionadas toohello administrador/coadministrador função global da assinatura hello, são adicionados o tooActive diretório como convidado. Nessa situação, você receberá um "você não tem permissões toocreate..." saudação de aviso **adicionar conta de automação** folha. Os usuários que foram adicionados toohello administrador/coadministrador função global primeiro pode ser removida da instância do Active Directory da assinatura hello e adicionado novamente toomake-los como um usuário completo no Active Directory. tooverify nesta situação, do hello **Active Directory do Azure** painel Olá portal do Azure, selecione **usuários e grupos**, selecione **todos os usuários** e, depois de selecionar Olá usuário específico, selecione **perfil**. Olá valor Olá **o tipo de usuário** atributo sob o perfil de usuários Olá não deve ser iguais **convidado**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Criar uma nova conta de automação de saudação portal do Azure
Nesta seção, execute Olá seguindo as etapas toocreate uma conta de automação do Azure no portal do Azure de saudação.    

1. Entrar toohello portal do Azure com uma conta que seja membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.
2. Clique em **Novo**.<br><br> ![Selecione a opção Novo no portal do Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Procurar **automação** e, em seguida, em Olá resultados da pesquisa selecione **controle e automação***.<br><br> ![Pesquise e selecione Automação no Marketplace](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. Na folha de contas de automação hello, clique em **adicionar**.<br><br>![Adicionar Conta de Automação](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Se você vir Olá após o aviso na Olá **adicionar conta de automação** folha, é porque sua conta não é um membro da função de administradores de assinatura hello e coadministrador da assinatura de saudação.<br><br>![Aviso Adicionar Conta de Automação](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. Em Olá **adicionar conta de automação** folha em Olá **nome** caixa, digite um nome para sua nova conta de automação.
5. Se você tiver mais de uma assinatura, especifique uma nova conta de saudação, um novo ou existente **grupo de recursos** e um datacenter do Azure **local**.
6. Verifique se o valor de saudação **Sim** é selecionado para Olá **criar Azure conta executar como** opção e, em seguida, clique em Olá **criar** botão.  
   
   > [!NOTE]
   > Se você escolher toonot criar conta executar como da saudação selecionando a opção de saudação **não**, você verá uma mensagem de aviso em Olá **adicionar conta de automação** folha.  Enquanto Olá conta é criada no hello portal do Azure, ele não tem uma identidade de autenticação correspondente dentro de sua clássico ou serviço de diretório de assinatura do Gerenciador de recursos e, portanto, nenhum tooresources de acesso na sua assinatura.  Isso impede que qualquer runbooks fazendo referência a essa conta seja capaz de tooauthenticate e executar tarefas com base nos recursos nesses modelos de implantação.
   > 
   > ![Aviso Adicionar Conta de Automação](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Quando a entidade de serviço Olá não é criada a função de Colaborador de saudação não está atribuída.
   > 

7. Enquanto o Azure cria a conta de automação hello, você pode acompanhar o progresso de saudação em **notificações** menu hello.

### <a name="resources-included"></a>Recursos incluídos
Quando a conta de automação de saudação é criada com êxito, vários recursos são criados automaticamente para você.  Olá, a tabela a seguir resume os recursos para Olá conta executar como.<br>

| Recurso | Descrição |
| --- | --- |
| Runbook AzureAutomationTutorial |Um runbook gráfico de exemplo que demonstra como usar tooauthenticate Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação. |
| Runbook do AzureAutomationTutorialScript |Um runbook do PowerShell de exemplo que demonstra como usar tooauthenticate Olá conta executar como e obtém todos os recursos do Gerenciador de recursos de saudação. |
| AzureRunAsCertificate |Ativo de certificado criado durante a criação de conta de automação automaticamente ou usando o script do PowerShell Olá abaixo de uma conta existente.  Ele permite que você tooauthenticate com o Azure para que você possa gerenciar recursos do Gerenciador de recursos do Azure de runbooks.  Esse certificado tem um tempo de vida de um ano. |
| AzureRunAsConnection |Ativo de Conexão automaticamente criado durante a criação de conta de automação ou usando o script do PowerShell Olá abaixo de uma conta existente. |

Olá a tabela a seguir resume os recursos para Olá clássico executar como da conta.<br>

| Recurso | Descrição |
| --- | --- |
| Runbook do AzureClassicAutomationTutorial |Um exemplo gráfica de runbook, que obtém todas as máquinas virtuais clássicas Olá em uma assinatura usando Olá clássico conta executar como (certificado) e, em seguida, gera o status e o nome da VM hello. |
| Runbook do script AzureClassicAutomationTutorial |Um exemplo do PowerShell de runbook, que obtém todas as máquinas virtuais clássicas Olá em uma assinatura usando Olá clássico conta executar como (certificado) e, em seguida, gera o status e o nome da VM hello. |
| AzureClassicRunAsCertificate |Ativo de certificado que é criado automaticamente usado tooauthenticate com o Azure para que você pode gerenciar recursos clássicos do Azure em runbooks.  Esse certificado tem um tempo de vida de um ano. |
| AzureClassicRunAsConnection |Ativo de Conexão que é criado automaticamente usado tooauthenticate com o Azure para que você pode gerenciar recursos clássicos do Azure em runbooks. |


## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a criação de gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).
* tooget iniciado com runbooks do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md).
