---
title: "Tutorial: integração do Azure Active Directory ao Concur | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="263c5-103">Tutorial: configurar o Concur para provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="263c5-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="263c5-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Concur e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="263c5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="263c5-105">Prerequisites</span></span>

<span data-ttu-id="263c5-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="263c5-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="263c5-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="263c5-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="263c5-108">Uma assinatura habilitada para logon único do Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="263c5-109">Uma conta de usuário no Concur com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="263c5-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="263c5-110">Como atribuir usuários ao Concur</span><span class="sxs-lookup"><span data-stu-id="263c5-110">Assigning users to Concur</span></span>

<span data-ttu-id="263c5-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="263c5-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="263c5-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="263c5-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="263c5-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao seu aplicativo Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="263c5-114">Depois de decidir, atribua esses usuários ao seu aplicativo Concur seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="263c5-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="263c5-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="263c5-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="263c5-116">Dicas importantes para atribuir usuários ao Concur</span><span class="sxs-lookup"><span data-stu-id="263c5-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="263c5-117">Recomendamos a atribuição de um único usuário do Azure AD ao Concur para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="263c5-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="263c5-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="263c5-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="263c5-119">Ao atribuir um usuário ao Concur, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="263c5-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="263c5-120">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="263c5-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="263c5-121">Permitir provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="263c5-121">Enable user provisioning</span></span>

<span data-ttu-id="263c5-122">Esta seção orienta você pela conexão do Azure AD com a API de provisionamento de conta de usuário do Concur e pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Concur com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="263c5-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="263c5-123">Você também pode optar por habilitar o logon único baseado em SAML para o Concur, seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="263c5-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="263c5-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="263c5-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="263c5-125">Para configurar o provisionamento de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="263c5-125">To configure user account provisioning:</span></span>

<span data-ttu-id="263c5-126">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="263c5-127">Para habilitar os aplicativos no serviço de Despesas, é necessário configurar e usar um perfil de Administrador de Serviço Web.</span><span class="sxs-lookup"><span data-stu-id="263c5-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="263c5-128">Não adicione a função de Administrador de WS ao seu perfil de administrador existente usado para as funções administrativas de T&E.</span><span class="sxs-lookup"><span data-stu-id="263c5-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="263c5-129">O consultor do Concur ou o administrador do cliente deve criar um perfil de Administrador de Serviços Web distinto e o administrador do cliente deve usar esse perfil para as funções de Administrador de Serviços Web (por exemplo, habilitação de aplicativos).</span><span class="sxs-lookup"><span data-stu-id="263c5-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="263c5-130">Esses perfis devem ser mantidos separados do perfil de administração diária de T&E do administrador do cliente (o perfil de administração de T&E não deve ter a função de Administrador de Serviço Web).</span><span class="sxs-lookup"><span data-stu-id="263c5-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="263c5-131">Ao criar o perfil que será usado para habilitar o aplicativo, insira o nome do administrador do cliente nos campos de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="263c5-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="263c5-132">Isso atribuirá propriedade ao perfil.</span><span class="sxs-lookup"><span data-stu-id="263c5-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="263c5-133">Depois que um ou mais perfis forem criados, o cliente deverá fazer logon com esse perfil para clicar no botão “*Habilitar*” de um Aplicativo do Parceiro no menu dos Serviços Web.</span><span class="sxs-lookup"><span data-stu-id="263c5-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="263c5-134">Essa ação não deve ser feita com o perfil usado para a administração normal de T&E pelos seguintes motivos.</span><span class="sxs-lookup"><span data-stu-id="263c5-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="263c5-135">É o cliente que deve clicar em “*Sim*” na janela do diálogo exibida após a habilitação de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="263c5-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="263c5-136">Esse clique confirma que o cliente está disposto a permitir que o Aplicativo parceiro acesse seus dados, portanto você ou o Parceiro não pode clicar no botão Sim.</span><span class="sxs-lookup"><span data-stu-id="263c5-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="263c5-137">Se um administrador de cliente que habilitou um aplicativo usando o perfil de administrador de T&E deixar a empresa (resultando na inativação do perfil), qualquer aplicativo habilitado com esse perfil não funcionará até que seja habilitado com outro perfil ativo de Administrador de WS.</span><span class="sxs-lookup"><span data-stu-id="263c5-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="263c5-138">É por isso que você deve criar perfis de Administrador de Serviços Web distintos.</span><span class="sxs-lookup"><span data-stu-id="263c5-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="263c5-139">Se um administrador deixar a empresa, o nome associado ao perfil de Administrador de WS pode ser alterado para o administrador substituto, se isso for desejado, sem afetar o aplicativo habilitado, porque esse perfil não ficará inativado.</span><span class="sxs-lookup"><span data-stu-id="263c5-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="263c5-140">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="263c5-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="263c5-141">Faça logon em seu locatário do **Concur**.</span><span class="sxs-lookup"><span data-stu-id="263c5-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="263c5-142">No menu **Administração**, selecione **Serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="263c5-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="263c5-143">![Locatário do Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Locatário do Concur")</span><span class="sxs-lookup"><span data-stu-id="263c5-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="263c5-144">No lado esquerdo, no painel **Serviços Web**, selecione **Habilitar Aplicativo do Parceiro**.</span><span class="sxs-lookup"><span data-stu-id="263c5-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="263c5-145">![Habilitar Aplicativo do Parceiro](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar Aplicativo do Parceiro")</span><span class="sxs-lookup"><span data-stu-id="263c5-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="263c5-146">Na lista **Habilitar Aplicativo**, selecione **Azure Active Directory** e clique em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="263c5-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="263c5-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="263c5-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="263c5-148">Clique em **Sim** para fechar o diálogo **Confirmar Ação**.</span><span class="sxs-lookup"><span data-stu-id="263c5-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="263c5-149">![Confirmar Ação](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar Ação")</span><span class="sxs-lookup"><span data-stu-id="263c5-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="263c5-150">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="263c5-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="263c5-151">Se você já tiver configurado o Concur para logon único, pesquise sua instância do Concur usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="263c5-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="263c5-152">Caso contrário, selecione **Adicionar** e pesquise **Concur** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="263c5-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="263c5-153">Selecione o Concur nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="263c5-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="263c5-154">Selecione sua instância do Concur e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="263c5-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="263c5-155">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="263c5-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![provisionamento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="263c5-157">Na seção **Credenciais do Administrador**, insira o **nome de usuário** e a **senha** do administrador do Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="263c5-158">No Portal do Azure, clique em **Testar Conexão** para garantir que o Azure AD possa se conectar ao seu aplicativo Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="263c5-159">Se a conexão falhar, verifique se a sua conta do Concur tem permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="263c5-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="263c5-160">Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="263c5-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="263c5-161">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="263c5-161">Click **Save.**</span></span>

14. <span data-ttu-id="263c5-162">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Concur.**</span><span class="sxs-lookup"><span data-stu-id="263c5-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="263c5-163">Na seção **Mapeamentos de Atributo**, revise os atributos de usuário que serão sincronizados do Azure AD para o Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="263c5-164">Os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário no Concur para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="263c5-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="263c5-165">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="263c5-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="263c5-166">Para habilitar o serviço de provisionamento do Azure AD para o Concur, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="263c5-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="263c5-167">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="263c5-167">Click **Save.**</span></span>

<span data-ttu-id="263c5-168">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="263c5-168">You can now create a test account.</span></span> <span data-ttu-id="263c5-169">Aguarde 20 minutos para verificar se a conta foi sincronizada com o Concur.</span><span class="sxs-lookup"><span data-stu-id="263c5-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="263c5-170">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="263c5-170">Additional resources</span></span>

* [<span data-ttu-id="263c5-171">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="263c5-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="263c5-172">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="263c5-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="263c5-173">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="263c5-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

