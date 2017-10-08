---
title: aaaCreate identidade para o aplicativo no portal do Azure | Microsoft Docs
description: "Descreve como toocreate um novo aplicativo do Active Directory do Azure e o serviço principal que pode ser usado com o controle de acesso baseado em função hello no Gerenciador de recursos do Azure toomanage acessam tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Use o portal toocreate um aplicativo do Azure Active Directory e a entidade de serviço que pode acessar os recursos

Quando você tiver um aplicativo que precisa tooaccess ou modificar os recursos, você deve configurar um aplicativo do Azure AD (Active Directory) e atribuir Olá necessárias permissões tooit. Essa abordagem é preferível toorunning Olá aplicativo com suas próprias credenciais, porque:

* Você pode atribuir permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões. Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.
* Você não tem credenciais do aplicativo de saudação toochange se alterar suas responsabilidades. 
* Você pode usar uma autenticação de certificado de tooautomate ao executar um script autônomo.

Este tópico mostra como tooperform aqueles percorre portal hello. Ele se concentra em um aplicativo de único locatário em que o aplicativo hello é pretendido toorun dentro de uma só organização. Você normalmente usa os aplicativos com um único locatário para os aplicativos da linha de negócios executados em sua organização.
 
## <a name="required-permissions"></a>Permissões necessárias
toocomplete neste tópico, você deve ter um aplicativo de tooregister de permissões suficientes com seu locatário do AD do Azure e atribuir a função de tooa aplicativo hello em sua assinatura do Azure. Vamos garantir que você tenha Olá permissões corretas tooperform essas etapas.

### <a name="check-azure-active-directory-permissions"></a>Verificar as permissões do Azure Active Directory
1. Fazer logon no tooyour conta do Azure por meio de saudação [portal do Azure](https://portal.azure.com).
2. Selecione **Azure Active Directory**.

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. No Azure Active Directory, selecione **Configurações de Usuário**.

     ![selecionar configurações de usuário](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Verificar Olá **registros do aplicativo** configuração. Se definir muito**Sim**, os usuários não administradores podem registrar aplicativos do AD. Essa configuração significa que qualquer usuário no locatário do AD do Azure Olá pode registrar um aplicativo. Você pode continuar muito[permissões de assinatura do Azure verificar](#check-azure-subscription-permissions).

     ![exibir registros de aplicativo](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Se os registros do aplicativo hello configuração está definido muito**não**, somente os usuários administrativos podem registrar aplicativos. É necessário toocheck se sua conta é um administrador de locatário do AD do Azure hello. Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
6. Procure por sua conta e selecione-a quando encontrá-la.

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png)
7. Para sua conta, selecione **função de diretório**. 

     ![função de diretório](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Veja sua função de diretório atribuída no Azure AD. Se sua conta é atribuída a função de usuário toohello, mas hello, configuração de registro de aplicativo (da saudação etapas anteriores) é limitado tooadmin usuários, peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.

     ![exibir função](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Verificar permissões de assinatura do Azure
Sua assinatura do Azure, sua conta deve ter `Microsoft.Authorization/*/Write` acessar tooassign uma função de tooa de aplicativo do AD. Essa ação é concedida por meio de saudação [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) função ou [administrador de acesso do usuário](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) função. Se sua conta é atribuída toohello **Colaborador** função, você não tem permissão suficiente. Você receberá um erro durante a tentativa de função de principal tooa tooassign Olá serviço. 

toocheck suas permissões de assinatura:

1. Se você estiver não já em sua conta do AD do Azure de saudação etapas anteriores, selecione **Active Directory do Azure** no painel esquerdo do hello.

2. Encontre sua conta do Azure AD. Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
2. Procure por sua conta e selecione-a quando encontrá-la.

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Selecione **Recursos do Azure**.

     ![selecionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Exibir as funções atribuídas e determinar se você tem as permissões adequadas tooassign uma função de tooa de aplicativo do AD. Se não, peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser. Olá a imagem a seguir, o usuário de Olá é função proprietário toohello atribuído para duas assinaturas, que significa que o usuário tem permissões suficientes. 

     ![mostrar permissões](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Criar um aplicativo do Azure Active Directory
1. Fazer logon no tooyour conta do Azure por meio de saudação [portal do Azure](https://portal.azure.com).
2. Selecione **Azure Active Directory**.

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Selecione **Registros do Aplicativo**.   

     ![selecionar registros do aplicativo](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Selecione **Adicionar**.

     ![adicionar aplicativo](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Forneça um nome e uma URL para o aplicativo hello. Selecione **aplicativo Web / API** ou **nativo** para o tipo de saudação do aplicativo que você deseja toocreate. Depois de definir os valores hello, selecione **criar**.

     ![nomear aplicativo](./media/resource-group-create-service-principal-portal/create-app.png)

Você criou seu aplicativo.

## <a name="get-application-id-and-authentication-key"></a>Obter chave de autenticação e ID do aplicativo
Ao fazer logon por meio de programação, é necessário Olá ID para seu aplicativo e uma chave de autenticação. tooget esses valores, Olá use as etapas a seguir:

1. Em **Registros do Aplicativo** no Azure Active Directory, selecione seu aplicativo.

     ![selecionar aplicativo](./media/resource-group-create-service-principal-portal/select-app.png)
2. Saudação de cópia **ID do aplicativo** e armazená-la no código do aplicativo. Olá aplicativos Olá [aplicativos de exemplo](#sample-applications) seção Consulte valor toothis como id de saudação do cliente.

     ![ID do CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. toogenerate uma chave de autenticação, selecione **chaves**.

     ![selecionar chaves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Forneça uma descrição da chave de saudação e uma duração para a chave de saudação. Ao terminar, escolha **Salvar**.

     ![salvar chave](./media/resource-group-create-service-principal-portal/save-key.png)

     Depois de salvar chave hello, Olá valor chave Olá é exibido. Copie esse valor, porque não é capaz de tooretrieve chave de saudação mais tarde. Você fornece o valor de chave Olá Olá toolog de ID de aplicativo em como o aplicativo hello. Armazena o valor de chave Olá onde seu aplicativo pode recuperá-lo.

     ![chave salva](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Obter a ID do locatário
Quando programaticamente o logon, é preciso toopass Olá locatário ID com a solicitação de autenticação. 

1. ID de locatário Olá tooget, selecione **propriedades** para seu locatário do AD do Azure. 

     ![selecionar propriedades do Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Saudação de cópia **ID de diretório**. Esse valor é a ID do locatário.

     ![ID do locatário](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Atribuir o aplicativo toorole
tooaccess recursos em sua assinatura, você deve atribuir a função de tooa aplicativo hello. Decida qual função representa permissões corretas de saudação para o aplicativo hello. toolearn sobre as funções disponíveis do hello, consulte [RBAC: criado em funções](../active-directory/role-based-access-built-in-roles.md).

Você pode definir o escopo de saudação no nível de saudação de assinatura de saudação, o grupo de recursos ou o recurso. As permissões são herdadas toolower níveis de escopo. Por exemplo, adicionar que uma função de leitor de toohello de aplicativo para um grupo de recursos significa que ele pode ler o grupo de recursos hello e recursos que ela contém.

1. Navegar um nível de toohello de escopo que você deseja que o aplicativo hello tooassign. Por exemplo, tooassign uma função no escopo de assinatura hello, selecione **assinaturas**. Em vez disso, você pode selecionar um grupo de recursos ou um recurso.

     ![selecione a assinatura](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Selecione Olá determinada assinatura (grupo de recursos ou recursos) tooassign Olá aplicativo.

     ![selecionar assinatura para atribuição](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Selecione **Controle de Acesso (IAM)**.

     ![selecionar acesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Selecione **Adicionar**.

     ![escolher adicionar](./media/resource-group-create-service-principal-portal/select-add.png)
6. Selecione a função de saudação desejar tooassign toohello aplicativo. Olá, imagem a seguir mostra Olá **leitor** função.

     ![escolher função](./media/resource-group-create-service-principal-portal/select-role.png)

8. Procure seu aplicativo e selecione-o.

     ![pesquisar aplicativo](./media/resource-group-create-service-principal-portal/search-app.png)
9. Selecione **Okey** toofinish atribuição de função hello. Consulte o seu aplicativo na lista de saudação de usuários atribuídos a função tooa para esse escopo.

## <a name="log-in-as-hello-application"></a>Faça logon como um aplicativo hello

Seu aplicativo agora está configurado no Azure Active Directory. Você tem uma ID e uma chave toouse para fazer logon como um aplicativo hello. aplicativo Hello é designado como tooa que concede determinadas ações que ele possa executar. Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [CLI do Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Próximas etapas
* tooset um aplicativo multilocatário, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).
* toolearn sobre como especificar políticas de segurança, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).  
* Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
