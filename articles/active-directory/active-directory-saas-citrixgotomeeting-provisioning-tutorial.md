---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="bb044-103">Tutorial: Configurar o Citrix GoToMeeting para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="bb044-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="bb044-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Citrix GoToMeeting e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bb044-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb044-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bb044-105">Prerequisites</span></span>

<span data-ttu-id="bb044-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="bb044-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bb044-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bb044-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="bb044-108">Uma assinatura do Citrix GoToMeeting habilitada para logon único.</span><span class="sxs-lookup"><span data-stu-id="bb044-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="bb044-109">Uma conta de usuário no Citrix GoToMeeting com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="bb044-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="bb044-110">Atribuir usuários ao Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bb044-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="bb044-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="bb044-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bb044-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="bb044-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bb044-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao seu aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bb044-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="bb044-114">Depois de decidir, você pode atribuir esses usuários ao seu aplicativo Citrix GoToMeeting seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="bb044-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="bb044-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="bb044-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="bb044-116">Dicas importantes para atribuir usuários ao Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="bb044-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="bb044-117">Recomendamos atribuir um único usuário do Azure AD ao Citrix GoToMeeting para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="bb044-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="bb044-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="bb044-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bb044-119">Ao atribuir um usuário ao Citrix GoToMeeting, você precisa selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="bb044-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="bb044-120">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="bb044-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="bb044-121">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="bb044-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="bb044-122">Esta seção orienta você quanto à conexão do Azure AD com a API de provisionamento de conta de usuário do Citrix GoToMeeting e à configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Citrix GoToMeeting com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb044-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bb044-123">Você também pode optar por habilitar o logon único baseado em SAML para o Citrix GoToMeeting seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb044-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bb044-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="bb044-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="bb044-125">Para configurar o provisionamento automático de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="bb044-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="bb044-126">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bb044-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="bb044-127">Se já tiver configurado o Citrix GoToMeeting para logon único, pesquise por sua instância do Citrix GoToMeeting usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="bb044-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="bb044-128">Caso contrário, selecione **Adicionar** e pesquise por **Citrix GoToMeeting** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bb044-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="bb044-129">Selecione o Citrix GoToMeeting nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bb044-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="bb044-130">Selecione sua instância do Citrix GoToMeeting e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="bb044-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="bb044-131">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="bb044-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bb044-133">Na seção “Credenciais de Administrador”, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bb044-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="bb044-134">a.</span><span class="sxs-lookup"><span data-stu-id="bb044-134">a.</span></span> <span data-ttu-id="bb044-135">Na caixa de texto **Nome de Usuário do Administrador do Citrix GoToMeeting** , digite o nome de usuário de um administrador.</span><span class="sxs-lookup"><span data-stu-id="bb044-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="bb044-136">b.</span><span class="sxs-lookup"><span data-stu-id="bb044-136">b.</span></span> <span data-ttu-id="bb044-137">Na caixa de texto **Senha do Administrador do Citrix GoToMeeting** , digite a senha do administrador.</span><span class="sxs-lookup"><span data-stu-id="bb044-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="bb044-138">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD possa se conectar ao seu aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bb044-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="bb044-139">Se a conexão falhar, verifique se a sua conta do Citrix GoToMeeting tem permissões de Administrador de Equipe e repita a etapa **"Credenciais de Administrador"**.</span><span class="sxs-lookup"><span data-stu-id="bb044-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="bb044-140">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="bb044-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="bb044-141">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="bb044-141">Click **Save.**</span></span>

9. <span data-ttu-id="bb044-142">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Citrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="bb044-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="bb044-143">Na seção **Mapeamentos de Atributos**, revise os atributos de usuário que serão sincronizados do Azure AD para o Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bb044-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="bb044-144">Os atributos selecionados como propriedades **Correspondentes** serão usados para fazer a correspondência das contas de usuário no Citrix GoToMeeting para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="bb044-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="bb044-145">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="bb044-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="bb044-146">Para habilitar o serviço de provisionamento do Azure AD para o Citrix GoToMeeting, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="bb044-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="bb044-147">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="bb044-147">Click **Save.**</span></span>

<span data-ttu-id="bb044-148">Isso iniciará a sincronização inicial dos usuários e/ou grupos atribuídos ao Citrix GoToMeeting na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="bb044-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="bb044-149">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="bb044-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="bb044-150">Use a seção **Detalhes da Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="bb044-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb044-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bb044-151">Additional resources</span></span>

* [<span data-ttu-id="bb044-152">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="bb044-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb044-153">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb044-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bb044-154">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="bb044-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


