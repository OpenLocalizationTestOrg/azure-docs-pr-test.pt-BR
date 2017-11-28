---
title: "Tutorial: Configurando o LucidChart para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário para o LucidChart."
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
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="9a47b-103">Tutorial: Configurando o LucidChart para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="9a47b-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="9a47b-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no LucidChart e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9a47b-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9a47b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a47b-105">Prerequisites</span></span>

<span data-ttu-id="9a47b-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9a47b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9a47b-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a47b-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="9a47b-108">Um locatário do LucidChart com o [plano Enterprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou outro melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="9a47b-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="9a47b-109">Uma conta de usuário no LucidChart com permissões de Administrador</span><span class="sxs-lookup"><span data-stu-id="9a47b-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="9a47b-110">Atribuindo usuários ao LucidChart</span><span class="sxs-lookup"><span data-stu-id="9a47b-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="9a47b-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="9a47b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9a47b-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="9a47b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="9a47b-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9a47b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="9a47b-114">Depois de decidir, atribua esses usuários ao aplicativo LucidChart seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="9a47b-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="9a47b-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="9a47b-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="9a47b-116">Dicas importantes para atribuir usuários ao LucidChart</span><span class="sxs-lookup"><span data-stu-id="9a47b-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="9a47b-117">Recomendamos a atribuição de um único usuário do Azure AD ao LucidChart para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="9a47b-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="9a47b-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9a47b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9a47b-119">Ao atribuir um usuário ao LucidChart, é necessário selecionar a função **Usuário** ou outra função válida específica ao aplicativo (se disponível) na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="9a47b-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="9a47b-120">A função **Acesso Padrão** não funciona para o provisionamento e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="9a47b-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="9a47b-121">Configurando o provisionamento de usuário para o LucidChart</span><span class="sxs-lookup"><span data-stu-id="9a47b-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="9a47b-122">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do LucidChart e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no LucidChart, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a47b-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9a47b-123">Você também pode optar por habilitar o Logon Único baseado em SAML no LucidChart, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a47b-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9a47b-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="9a47b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="9a47b-125">Configurar o provisionamento automático de conta de usuário para o LucidChart no Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a47b-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="9a47b-126">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="9a47b-127">Se você já tiver configurado o LucidChart para logon único, pesquise a instância do LucidChart usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9a47b-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="9a47b-128">Caso contrário, selecione **Adicionar** e pesquise **LucidChart** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9a47b-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="9a47b-129">Selecione o LucidChart nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9a47b-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9a47b-130">Selecione a instância do LucidChart e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9a47b-131">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Provisionamento do LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="9a47b-133">Na seção **Credenciais de Administrador**, insira o **Token Secreto** gerado pela conta do LucidChart (o token pode ser encontrado em sua conta: **Equipe** > **Integração de Aplicativos** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="9a47b-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Provisionamento do LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="9a47b-135">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9a47b-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="9a47b-136">Se a conexão falhar, verifique se sua conta do LucidChart tem permissões de Administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="9a47b-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="9a47b-137">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção “Enviar uma notificação por email quando ocorrer uma falha”.</span><span class="sxs-lookup"><span data-stu-id="9a47b-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="9a47b-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-138">Click **Save**.</span></span> 

9. <span data-ttu-id="9a47b-139">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o LucidChart**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="9a47b-140">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o LucidChart.</span><span class="sxs-lookup"><span data-stu-id="9a47b-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="9a47b-141">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do LucidChart em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="9a47b-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="9a47b-142">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9a47b-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="9a47b-143">Para habilitar o serviço de provisionamento do Azure AD no LucidChart, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="9a47b-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="9a47b-144">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9a47b-144">Click **Save**.</span></span> 

<span data-ttu-id="9a47b-145">Essa operação inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao LucidChart na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="9a47b-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="9a47b-146">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="9a47b-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9a47b-147">É possível usar a seção **Detalhes de Sincronização** para monitorar o andamento e seguir os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="9a47b-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="9a47b-148">Para obter mais informações sobre como ler os logs de provisionamento do Azure AD, consulte [Relatando o provisionamento automático de conta de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="9a47b-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9a47b-149">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9a47b-149">Additional resources</span></span>

* [<span data-ttu-id="9a47b-150">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="9a47b-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="9a47b-151">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a47b-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="9a47b-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a47b-152">Next steps</span></span>

* [<span data-ttu-id="9a47b-153">Saiba como fazer revisão de logs e obter relatórios sobre atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="9a47b-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
