---
title: "Tutorial: Configurar o Slack para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário no Slack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="68991-103">Tutorial: Configurar o Slack para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="68991-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="68991-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Slack e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68991-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68991-105">Prerequisites</span></span>

<span data-ttu-id="68991-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="68991-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="68991-107">Um locatário de diretório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68991-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="68991-108">Um locatário do Slack com o [plano Plus](https://aadsyncfabric.slack.com/pricing), ou outro com mais recursos, habilitado</span><span class="sxs-lookup"><span data-stu-id="68991-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="68991-109">Uma conta de usuário no Slack com permissões de Administrador de Equipe</span><span class="sxs-lookup"><span data-stu-id="68991-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="68991-110">Observação: a integração de provisionamento do Azure AD depende da [API de SCIM do Slack](https://api.slack.com/scim), disponível para as equipes do Slack no plano Plus ou outro melhor.</span><span class="sxs-lookup"><span data-stu-id="68991-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="68991-111">Como atribuir usuários ao Slack</span><span class="sxs-lookup"><span data-stu-id="68991-111">Assigning users to Slack</span></span>

<span data-ttu-id="68991-112">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="68991-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="68991-113">No contexto do provisionamento automático de conta de usuário, somente os usuários e grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="68991-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="68991-114">Antes de configurar e habilitar o serviço de provisionamento, você precisará decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao seu aplicativo Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="68991-115">Depois de decidir, atribua esses usuários ao seu aplicativo Slack seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="68991-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="68991-116">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="68991-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="68991-117">Dicas importantes para atribuir usuários ao Slack</span><span class="sxs-lookup"><span data-stu-id="68991-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="68991-118">Recomendamos a atribuição de um único usuário do Azure AD ao Slack para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="68991-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="68991-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="68991-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="68991-120">Ao atribuir um usuário ao Slack, selecione a função **Usuário** ou "Grupo" na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="68991-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="68991-121">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="68991-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="68991-122">Como configurar o provisionamento de usuários no Slack</span><span class="sxs-lookup"><span data-stu-id="68991-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="68991-123">Esta seção orienta você pela conexão do Azure AD com a API de provisionamento de conta de usuário do Slack e pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Slack com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68991-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="68991-124">**Dica:** você também pode optar por habilitar o SSO baseado em SAML para o Slack seguindo as instruções fornecidas no (Portal do Azure) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="68991-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="68991-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="68991-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="68991-126">Para configurar o provisionamento automático de usuário para o Slack no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="68991-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="68991-127">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="68991-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="68991-128">Se você já tiver configurado o Slack para logon único, procure sua instância do Slack usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="68991-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="68991-129">Caso contrário, selecione **Adicionar** e procure **Slack** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="68991-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="68991-130">Selecione o Slack nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="68991-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="68991-131">Selecione sua instância do Slack e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="68991-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="68991-132">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="68991-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Provisionamento do Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="68991-134">Na seção **Credenciais de Administrador**, clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="68991-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="68991-135">Isso abre uma caixa de diálogo de autorização do Slack em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="68991-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="68991-136">Na nova janela, entre no Slack usando sua conta de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="68991-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="68991-137">Na caixa de diálogo de autorização resultante, selecione a equipe do Slack para a qual você deseja habilitar o provisionamento e, em seguida, selecione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="68991-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="68991-138">Depois de concluído, retorne ao Portal do Azure para concluir a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="68991-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Caixa de diálogo Autorização](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="68991-140">No Portal do Azure, clique em **Testar Conexão** para garantir que o Azure AD possa se conectar ao seu aplicativo Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="68991-141">Se a conexão falhar, verifique se a sua conta do Slack tem permissões de Administrador de Equipe e repita a etapa "Autorizar".</span><span class="sxs-lookup"><span data-stu-id="68991-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="68991-142">Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="68991-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="68991-143">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="68991-143">Click **Save**.</span></span> 

10) <span data-ttu-id="68991-144">Na seção Mapeamentos, selecione **Sincronizar usuários do Azure Active Directory com o Slack**.</span><span class="sxs-lookup"><span data-stu-id="68991-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="68991-145">Na seção **Mapeamentos de Atributo**, revise os atributos de usuário que serão sincronizados do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="68991-146">Observe que os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário no Slack para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="68991-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="68991-147">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="68991-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="68991-148">Para habilitar o serviço de provisionamento do Azure AD para o Slack, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="68991-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="68991-149">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="68991-149">Click **Save**.</span></span> 

<span data-ttu-id="68991-150">Isso iniciará a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Slack na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="68991-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="68991-151">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 10 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="68991-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="68991-152">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="68991-153">[Opcional] Como configurar o provisionamento do objeto de grupo para o Slack</span><span class="sxs-lookup"><span data-stu-id="68991-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="68991-154">Opcionalmente, você pode habilitar o provisionamento de objetos de grupo do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="68991-155">Isso é diferente da "atribuição de grupos de usuários", pois o objeto de grupo real, junto com seus membros, será replicado do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="68991-156">Por exemplo, se você tiver um grupo chamado "Meu Grupo" no Azure AD, um grupo de idêntico chamado "Meu Grupos" será criado dentro do Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="68991-157">Para habilitar o provisionamento de objetos de grupo:</span><span class="sxs-lookup"><span data-stu-id="68991-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="68991-158">Na seção Mapeamentos, selecione **Sincronizar grupos do Azure Active Directory com o Slack**.</span><span class="sxs-lookup"><span data-stu-id="68991-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="68991-159">Na folha Mapeamento de Atributos, defina Habilitado como Sim.</span><span class="sxs-lookup"><span data-stu-id="68991-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="68991-160">Na seção **Mapeamentos de Atributo**, revise os atributos de grupo que serão sincronizados do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="68991-161">Observe que os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder os grupos no Slack para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="68991-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="68991-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="68991-162">Click **Save**.</span></span>

<span data-ttu-id="68991-163">Isso resulta na sincronização total de qualquer objeto de grupo atribuído ao Slack na seção **Usuários e Grupos** do Azure AD para o Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="68991-164">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo Slack.</span><span class="sxs-lookup"><span data-stu-id="68991-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="68991-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="68991-165">Additional Resources</span></span>

* [<span data-ttu-id="68991-166">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="68991-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="68991-167">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68991-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
