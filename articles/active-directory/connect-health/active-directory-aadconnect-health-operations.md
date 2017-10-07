---
title: "operações do Active Directory Connect Health aaaAzure"
description: "Este artigo descreve as operações adicionais que podem ser executadas após a implantação do Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Operações do Azure Active Directory Connect Health
Este tópico descreve Olá várias operações que você pode executar usando a integridade de conexão do Azure Active Directory (AD do Azure).

## <a name="enable-email-notifications"></a>Habilitar notificações por email
Você pode configurar notificações de email hello Azure AD Connect Health service toosend quando os alertas indicam que sua infraestrutura de identidade não está íntegra. Isso ocorre quando um alerta é gerado e quando ele é resolvido.

![Captura de tela das configurações de notificação por email do Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> As notificações por email são habilitadas por padrão.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>notificações de email tooenable do Azure AD Connect Health
1. Olá abrir **alertas** folha para serviço de saudação do qual você deseja tooreceive notificação por email.
2. Na barra de ação hello, clique em **as configurações de notificação**.
3. No comutador de notificação de email hello, selecione **ON**.
4. Marque a caixa de seleção de saudação se desejar que todas as notificações de email tooreceive administradores globais.
5. Se você quiser tooreceive notificações de email em qualquer outro endereço de email, especificá-los no hello **destinatários de Email adicionais** caixa. tooremove um endereço de email nesta lista, clique em entrada hello e selecione **excluir**.
6. toofinalize Olá alterações, clique em **salvar**. As alterações entram em vigor somente depois de salvar.

## <a name="delete-a-server-or-service-instance"></a>Excluir uma instância de serviço ou servidor

Em alguns casos, convém tooremove um servidor do que está sendo monitorado. Aqui está o que você precisa tooknow tooremove um servidor do serviço de integridade de conexão de saudação do AD do Azure.

Quando você está excluindo um servidor, lembre-se do seguinte hello:

* Essa ação interromperá a coleta de dados desse servidor. Este servidor será removido do hello serviço de monitoramento. Após esta ação, você não é capazes de tooview novos alertas, monitoramento ou dados de análise de uso para este servidor.
* Esta ação não desinstala Olá agente de integridade do seu servidor. Se você não tiver desinstalado Olá agente de integridade antes de executar essa etapa, você poderá ver erros relacionados toohello agente de integridade no servidor de saudação.
* Essa ação não exclui dados Olá já coletados neste servidor. Esses dados são excluídos de acordo com a política de retenção de dados do Azure de saudação.
* Depois de executar essa ação, se você quiser toostart monitoramento Olá mesmo servidor novamente, você deve desinstalar e reinstalar Olá agente de integridade neste servidor.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete um servidor do serviço de integridade de conexão de saudação do AD do Azure
Azure AD Connect Health para Serviços de Federação do Active Directory (AD FS) e Azure AD Connect (sincronização):

1. Olá abrir **servidor** folha da saudação **lista de servidores** folha selecionando toobe de nome do servidor de saudação removido.
2. Em Olá **servidor** folha, na barra de ação hello, clique em **excluir**.
3. Confirme digitando o nome do servidor de saudação na caixa de confirmação de saudação.
4. Clique em **Excluir**.

Azure AD Connect Health para Azure Active Directory Domain Services:

1. Olá abrir **controladores de domínio** painel.
2. Selecione Olá toobe de controlador de domínio removido.
3. Na barra de ação hello, clique em **excluir selecionado**.
4. Confirme o servidor de saudação do hello ação toodelete.
5. Clique em **Excluir**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Excluir uma instância de serviço do serviço do Azure AD Connect Health
Em alguns casos, convém tooremove uma instância de serviço. Aqui está o que você precisa tooknow tooremove um serviço da instância do serviço de integridade de conexão de saudação do AD do Azure.

Quando você estiver excluindo uma instância de serviço, lembre-se do seguinte hello:

* Essa ação remove a instância atual do serviço de saudação do hello serviço de monitoramento.
* Esta ação não desinstale ou remova Olá agente de integridade de qualquer um dos servidores de saudação que foram monitorados como parte desta instância de serviço. Se você não tiver desinstalado Olá agente de integridade antes de executar essa etapa, você verá erros relacionados toohello agente de integridade em servidores de saudação.
* Todos os dados dessa instância do serviço é excluído de acordo com a política de retenção de dados do Azure de saudação.
* Depois de executar esta ação, se você quiser toostart Olá serviço de monitoramento, desinstale e reinstale o hello agente de integridade em todos os servidores de saudação. Depois de executar esta ação, se você quiser toostart monitoramento Olá mesmo servidor novamente, desinstalar, reinstalar e registrar Olá agente de integridade no servidor.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete uma instância de serviço do serviço de integridade de conexão de saudação do AD do Azure
1. Olá abrir **Service** folha da saudação **lista serviço** folha selecionando o identificador de serviço de saudação (nome do farm) que você deseja tooremove.
2. Em Olá **servidor** folha, na barra de ação hello, clique em **excluir**.
3. Confirme digitando o nome do serviço Olá na caixa de confirmação da saudação (por exemplo: sts.contoso.com).
4. Clique em **Excluir**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Gerenciar acesso com controle de acesso baseado em função
[Controle de acesso baseado em função (RBAC)](../role-based-access-control-configure.md) de integridade de conexão do AD do Azure fornece acesso toousers e grupos que não são administradores globais. RBAC atribui funções toohello devem usuários e grupos e fornece um mecanismo que os administradores globais de saudação toolimit em seu diretório.

### <a name="roles"></a>Funções
Integridade de conexão do AD do Azure dá suporte a saudação funções internas a seguir:

| Função | Permissões |
| --- | --- |
| Proprietário |Os proprietários podem *gerenciar o acesso* (por exemplo, atribua um função tooa usuário ou grupo), *exibir todas as informações* (por exemplo, exibir alertas) do portal de saudação e *alterar configurações* ( Por exemplo, as notificações de email) dentro do Azure AD Connect Health. <br>Por padrão, os administradores globais do Azure AD são atribuídos a essa função e isso não pode ser alterado. |
| Colaborador |Colaboradores podem *exibir todas as informações* (por exemplo, exibir alertas) do portal de saudação e *alterar configurações* (por exemplo, as notificações por email) dentro do Azure AD Connect Health. |
| Leitor |Os leitores podem *exibir todas as informações* (por exemplo, exibir alertas) do portal hello dentro do Azure AD Connect Health. |

Todas as outras funções (como administradores de acesso de usuário ou usuários do DevTest Labs) não têm tooaccess nenhum impacto no Azure AD Connect Health, mesmo se as funções hello estão disponíveis na experiência do portal hello.

### <a name="access-scope"></a>Escopo de acesso
O Azure AD Connect Health dá suporte ao gerenciamento de acesso em dois níveis:

* **Todas as instâncias de serviço**: isso é hello recomendado caminho na maioria dos casos. Ele controla o acesso para todas as instâncias de serviço (por exemplo, um farm do AD FS) em todos os tipos de função que estão sendo monitorados pelo Azure AD Connect Health.
* **Instância de serviço**: em alguns casos, talvez seja necessário toosegregate acesso com base em tipos de função ou por uma instância de serviço. Nesse caso, você pode gerenciar o acesso no nível de instância de serviço hello.  

A permissão é concedida, se um usuário final tem acesso no diretório de saudação ou no serviço de nível de instância.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Permitir acesso de usuários ou grupos tooAzure AD Connect Health
Olá etapas a seguir mostram como tooallow acessar.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Etapa 1: Selecione o escopo de acesso apropriados Olá
tooallow um acesso de usuário no hello *todas as instâncias de serviço* nível dentro do Azure AD Connect Health, a folha principal Olá aberta no Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Etapa 2: Adicionar usuários e grupos e atribuir funções
1. De saudação **configurar** seção, clique em **usuários**.<br>
   ![Captura de tela da folha principal do RBAC do Azure AD Connect Health, com Usuários realçado](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Selecione **Adicionar**.
3. Em Olá **selecionar uma função** painel, selecione uma função (por exemplo, **proprietário**).<br>
   ![Captura de tela da janela Usuários do RBAC do Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Nome do tipo hello ou identificador de saudação destinada a usuário ou grupo. Você pode selecionar um ou mais usuários ou grupos de saudação simultaneamente. Clique em **Selecionar**.
   ![Captura de tela da janela Usuários do RBAC do Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Selecione **OK**.<br>
6. Após a conclusão da atribuição de função Olá, grupos e usuários de saudação aparecem na lista de saudação.<br>
   ![Captura de tela da janela Usuários do RBAC do Azure AD Connect Health, com Novos Usuários realçado](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Agora Olá listados os usuários e grupos têm acesso, de acordo com o tootheir funções atribuída.

> [!NOTE]
> * Os administradores globais têm sempre operações de saudação tooall acesso completo, mas as contas de administrador global não estão presentes no hello anterior da lista.
> * Não há suporte para o recurso de convidar usuários Hello dentro do Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Etapa 3: Local de folha de saudação do compartilhamento com usuários ou grupos
1. Depois que você atribuir permissões, o usuário poderá acessar o Azure AD Connect Health [aqui](http://aka.ms/aadconnecthealth).
2. Na folha de saudação usuário Olá pode fixar folha hello, ou partes diferentes do mesmo, toohello painel. Basta clicar Olá **toodashboard Pin** ícone.<br>
   ![Captura de tela da folha de fixar do RBAC do Azure AD Connect Health, com o ícone de pino realçado](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Um usuário com a função de leitor de saudação atribuído não é extensão do Azure AD Connect Health tooget capaz de saudação do Azure Marketplace. usuário Olá não é possível executar Olá necessário "criar" operação toodo assim. usuário Olá ainda pode obter toohello folha toohello vai precede o link. Para uso subsequente, usuário Olá pode fixar o dashboard de toohello de folha de saudação.
>
>

### <a name="remove-users-or-groups"></a>Remover usuários ou grupos
Você pode remover um usuário ou grupo adicionado tooAzure AD RBAC de integridade de conexão. Simplesmente Olá usuário ou grupo e selecione **remover**.<br>
![Captura de tela da janela Usuários do RBAC do Azure AD Connect Health, com Remover realçado](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Próximas etapas
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
