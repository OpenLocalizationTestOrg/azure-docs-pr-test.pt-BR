---
title: "Tutorial: Configurando o Samanage para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário para o Samanage."
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
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="0c208-103">Tutorial: Configurando o Samanage para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="0c208-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="0c208-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Samanage e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Samanage.</span><span class="sxs-lookup"><span data-stu-id="0c208-104">The objective of this tutorial is to show you the steps you need to perform in Samanage and Azure AD to automatically provision and de-provision user accounts from Azure AD to Samanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0c208-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c208-105">Prerequisites</span></span>

<span data-ttu-id="0c208-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0c208-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0c208-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c208-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="0c208-108">Um locatário do Samanage com o [plano Professional](https://www.samanage.com/pricing/) ou outro melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="0c208-108">A Samanage tenant with the [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="0c208-109">Uma conta de usuário no Samanage com permissões de Administrador</span><span class="sxs-lookup"><span data-stu-id="0c208-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="0c208-110">A integração de provisionamento do Azure AD depende da [API REST do Samanage](https://www.samanage.com/api/), disponível para as equipes do Samanage no plano Professional ou outro melhor.</span><span class="sxs-lookup"><span data-stu-id="0c208-110">The Azure AD provisioning integration relies on the [Samanage REST API](https://www.samanage.com/api/), which is available to Samanage teams on the Professional plan or better.</span></span>

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="0c208-111">Atribuindo usuários ao Samanage</span><span class="sxs-lookup"><span data-stu-id="0c208-111">Assigning users to Samanage</span></span>

<span data-ttu-id="0c208-112">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="0c208-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0c208-113">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="0c208-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="0c208-114">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Samanage.</span><span class="sxs-lookup"><span data-stu-id="0c208-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Samanage app.</span></span> <span data-ttu-id="0c208-115">Depois de decidir, atribua esses usuários ao aplicativo Samanage seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="0c208-115">Once decided, you can assign these users to your Samanage app by following the instructions here:</span></span>

[<span data-ttu-id="0c208-116">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="0c208-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="0c208-117">Dicas importantes para atribuir usuários ao Samanage</span><span class="sxs-lookup"><span data-stu-id="0c208-117">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="0c208-118">Recomendamos a atribuição de um único usuário do Azure AD ao Samanage para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c208-118">It is recommended that a single Azure AD user is assigned to Samanage to test the provisioning configuration.</span></span> <span data-ttu-id="0c208-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0c208-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0c208-120">Ao atribuir um usuário ao Samanage, é necessário selecionar a função **Usuário** ou outra função válida específica ao aplicativo (se disponível) na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="0c208-120">When assigning a user to Samanage, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="0c208-121">A função **Acesso Padrão** não funciona para o provisionamento e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="0c208-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="0c208-122">Como um recurso adicional, o serviço de provisionamento lê as funções personalizadas definidas no Samanage e importa-as para o Azure AD, no qual podem ser selecionadas na caixa de diálogo Selecionar Função.</span><span class="sxs-lookup"><span data-stu-id="0c208-122">As an added feature, the provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="0c208-123">Essas funções ficarão visíveis no Portal do Azure depois que o serviço de provisionamento for habilitado e um ciclo de sincronização for concluído.</span><span class="sxs-lookup"><span data-stu-id="0c208-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-samanage"></a><span data-ttu-id="0c208-124">Configurando o provisionamento de usuário para o Samanage</span><span class="sxs-lookup"><span data-stu-id="0c208-124">Configuring user provisioning to Samanage</span></span> 

<span data-ttu-id="0c208-125">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Samanage e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Samanage, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c208-125">This section guides you through connecting your Azure AD to Samanage's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0c208-126">Você também pode optar por habilitar o Logon Único baseado em SAML no Samanage, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c208-126">You may also choose to enabled SAML-based Single Sign-On for Samanage, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c208-127">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="0c208-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a><span data-ttu-id="0c208-128">Configurar o provisionamento automático de conta de usuário para o Samanage no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0c208-128">Configure automatic user account provisioning to Samanage in Azure AD:</span></span>


1. <span data-ttu-id="0c208-129">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0c208-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="0c208-130">Se você já tiver configurado o Samanage para logon único, pesquise a instância do Samanage usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0c208-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using the search field.</span></span> <span data-ttu-id="0c208-131">Caso contrário, selecione **Adicionar** e pesquise **Samanage** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0c208-131">Otherwise, select **Add** and search for **Samanage** in the application gallery.</span></span> <span data-ttu-id="0c208-132">Selecione o Samanage nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0c208-132">Select Samanage from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="0c208-133">Selecione a instância do Samanage e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="0c208-133">Select your instance of Samanage, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="0c208-134">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="0c208-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Provisionamento do Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="0c208-136">Na seção **Credenciais de Administrador**, insira o **Nome de Usuário e Senha do Administrador** de sua conta do Samanage.</span><span class="sxs-lookup"><span data-stu-id="0c208-136">Under the **Admin Credentials** section, input the **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="0c208-137">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo Samanage.</span><span class="sxs-lookup"><span data-stu-id="0c208-137">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Samanage app.</span></span> <span data-ttu-id="0c208-138">Se a conexão falhar, verifique se sua conta do Samanage tem permissões de Administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="0c208-138">If the connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="0c208-139">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção “Enviar uma notificação por email quando ocorrer uma falha”.</span><span class="sxs-lookup"><span data-stu-id="0c208-139">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="0c208-140">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0c208-140">Click **Save**.</span></span> 

9. <span data-ttu-id="0c208-141">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Samanage**.</span><span class="sxs-lookup"><span data-stu-id="0c208-141">Under the Mappings section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

10. <span data-ttu-id="0c208-142">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Samanage.</span><span class="sxs-lookup"><span data-stu-id="0c208-142">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Samanage.</span></span> <span data-ttu-id="0c208-143">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Samanage em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="0c208-143">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="0c208-144">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="0c208-144">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="0c208-145">Para habilitar o serviço de provisionamento do Azure AD no Samanage, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="0c208-145">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="0c208-146">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0c208-146">Click **Save**.</span></span> 

<span data-ttu-id="0c208-147">Essa operação inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Samanage na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="0c208-147">This operation starts the initial synchronization of any users and/or groups assigned to Samanage in the Users and Groups section.</span></span> <span data-ttu-id="0c208-148">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="0c208-148">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0c208-149">É possível usar a seção **Detalhes de Sincronização** para monitorar o andamento e seguir os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c208-149">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="0c208-150">Para obter mais informações sobre como ler os logs de provisionamento do Azure AD, consulte [Relatando o provisionamento automático de conta de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0c208-150">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0c208-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0c208-151">Additional resources</span></span>

* [<span data-ttu-id="0c208-152">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="0c208-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0c208-153">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c208-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="0c208-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c208-154">Next steps</span></span>

* [<span data-ttu-id="0c208-155">Saiba como fazer revisão de logs e obter relatórios sobre atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="0c208-155">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
