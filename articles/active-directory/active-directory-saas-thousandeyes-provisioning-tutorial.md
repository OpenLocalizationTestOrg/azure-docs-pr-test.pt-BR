---
title: "Tutorial: configurar o ThousandEyes para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário no ThousandEyes."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="fbb26-103">Tutorial: configurar o ThousandEyes para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="fbb26-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="fbb26-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no ThousandEyes e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fbb26-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fbb26-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fbb26-105">Prerequisites</span></span>

<span data-ttu-id="fbb26-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fbb26-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fbb26-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbb26-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="fbb26-108">Um locatário do ThousandEyes com o [Plano Standard](https://www.thousandeyes.com/pricing) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="fbb26-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="fbb26-109">Uma conta de usuário no ThousandEyes com permissões de administrador</span><span class="sxs-lookup"><span data-stu-id="fbb26-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="fbb26-110">A integração de provisionamento do Azure AD depende da [API de SCIM do ThousandEyes](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), disponível para as equipes do ThousandEyes no plano Standard ou outro melhor.</span><span class="sxs-lookup"><span data-stu-id="fbb26-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="fbb26-111">Atribuição de usuários ao ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fbb26-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="fbb26-112">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="fbb26-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fbb26-113">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="fbb26-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="fbb26-114">Antes de configurar e habilitar o serviço de provisionamento, é necessário decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao seu aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fbb26-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="fbb26-115">Depois de decidir, atribua esses usuários ao seu aplicativo ThousandEyes seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="fbb26-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="fbb26-116">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="fbb26-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="fbb26-117">Dicas importantes para atribuir usuários ao ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fbb26-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="fbb26-118">Recomendamos a atribuição de um único usuário do Azure AD ao ThousandEyes para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="fbb26-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="fbb26-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fbb26-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fbb26-120">Ao atribuir um usuário ao ThousandEyes, é necessário selecionar a função **Usuário** ou outra função válida específica do aplicativo (se disponível) na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="fbb26-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="fbb26-121">A função **Acesso Padrão** não funciona para o provisionamento e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="fbb26-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="fbb26-122">Configuração do provisionamento de usuários no ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="fbb26-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="fbb26-123">Esta seção explica como conectar seu Azure AD à API de provisionamento de conta de usuário do ThousandEyes e como configurar o serviço de provisionamento a fim de criar, atualizar e desabilitar contas de usuário atribuídas no ThousandEyes com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb26-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="fbb26-124">Você também pode optar por habilitar o logon único baseado em SAML para o ThousandEyes, seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbb26-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fbb26-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="fbb26-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="fbb26-126">Configurar o provisionamento automático de conta de usuário para o ThousandEyes no Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb26-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="fbb26-127">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="fbb26-128">Se você já tiver configurado o ThousandEyes para logon único, pesquise sua instância do ThousandEyes usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fbb26-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="fbb26-129">Caso contrário, selecione **Adicionar** e pesquise **ThousandEyes** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fbb26-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="fbb26-130">Selecione o ThousandEyes nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fbb26-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="fbb26-131">Selecione sua instância do ThousandEyes e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="fbb26-132">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="fbb26-134">Na seção **Credenciais de Administrador**, insira o **Token Secreto** gerado pela conta do ThousandEyes (é possível localizar o token na sua conta do ThousandEyes: **Segurança e Autenticação**).</span><span class="sxs-lookup"><span data-stu-id="fbb26-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="fbb26-136">No Portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD possa se conectar ao seu aplicativo ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fbb26-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="fbb26-137">Se a conexão falhar, verifique se sua conta do ThousandEyes tem permissões de Administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="fbb26-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="fbb26-138">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção “Enviar uma notificação por email quando ocorrer uma falha”.</span><span class="sxs-lookup"><span data-stu-id="fbb26-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="fbb26-139">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-139">Click **Save**.</span></span> 

9. <span data-ttu-id="fbb26-140">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="fbb26-141">Na seção **Mapeamentos de Atributo**, revise os atributos de usuário que serão sincronizados do Azure AD para o ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="fbb26-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="fbb26-142">Os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário no ThousandEyes para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="fbb26-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="fbb26-143">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="fbb26-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="fbb26-144">Para habilitar o serviço de provisionamento do Azure AD para o ThousandEyes, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="fbb26-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="fbb26-145">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fbb26-145">Click **Save**.</span></span> 

<span data-ttu-id="fbb26-146">Essa operação inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao ThousandEyes na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="fbb26-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="fbb26-147">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="fbb26-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fbb26-148">É possível usar a seção **Detalhes de Sincronização** para monitorar o andamento e seguir os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="fbb26-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="fbb26-149">Para obter mais informações sobre como ler os logs de provisionamento do Azure AD, consulte [Relatando o provisionamento automático de conta de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="fbb26-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fbb26-150">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fbb26-150">Additional resources</span></span>

* [<span data-ttu-id="fbb26-151">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="fbb26-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="fbb26-152">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbb26-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="fbb26-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbb26-153">Next steps</span></span>

* [<span data-ttu-id="fbb26-154">Saiba como fazer revisão de logs e obter relatórios sobre atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="fbb26-154">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
