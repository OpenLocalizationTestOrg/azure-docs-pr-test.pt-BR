---
title: "Tutorial: integração do Azure Active Directory com o DocuSign | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3b509ffa934949200277ae431761d2accd4a02d6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="fe412-103">Tutorial: Configurando o DocuSign para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="fe412-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="fe412-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no DocuSign e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe412-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe412-105">Prerequisites</span></span>

<span data-ttu-id="fe412-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fe412-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fe412-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe412-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="fe412-108">Uma assinatura habilitada para logon único do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="fe412-109">Uma conta de usuário no DocuSign com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="fe412-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="fe412-110">Atribuindo usuários ao DocuSign</span><span class="sxs-lookup"><span data-stu-id="fe412-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="fe412-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="fe412-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fe412-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="fe412-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="fe412-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="fe412-114">Depois de decidir, atribua esses usuários ao aplicativo DocuSign seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="fe412-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="fe412-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="fe412-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="fe412-116">Dicas importantes para atribuir usuários ao DocuSign</span><span class="sxs-lookup"><span data-stu-id="fe412-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="fe412-117">Recomendamos a atribuição de um único usuário do Azure AD ao DocuSign para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="fe412-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="fe412-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fe412-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fe412-119">Ao atribuir um usuário ao DocuSign, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="fe412-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="fe412-120">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="fe412-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="fe412-121">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="fe412-121">Enable User Provisioning</span></span>

<span data-ttu-id="fe412-122">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do DocuSign e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no DocuSign, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe412-122">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="fe412-123">Você também pode optar por habilitar o Logon Único baseado em SAML no DocuSign, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe412-123">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fe412-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="fe412-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="fe412-125">Para configurar o provisionamento de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="fe412-125">To configure user account provisioning:</span></span>

<span data-ttu-id="fe412-126">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="fe412-127">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fe412-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="fe412-128">Se você já tiver configurado o DocuSign para logon único, pesquise a instância do DocuSign usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fe412-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="fe412-129">Caso contrário, selecione **Adicionar** e pesquise **DocuSign** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fe412-129">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="fe412-130">Selecione o DocuSign nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fe412-130">Select DocuSign from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="fe412-131">Selecione a instância do DocuSign e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="fe412-131">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="fe412-132">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="fe412-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="fe412-134">Na seção **Credenciais de Administrador**, forneça as seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="fe412-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="fe412-135">a.</span><span class="sxs-lookup"><span data-stu-id="fe412-135">a.</span></span> <span data-ttu-id="fe412-136">Na caixa de texto **Nome de Usuário Administrador**, digite um nome de conta do DocuSign que tem o perfil **Administrador do Sistema** atribuído no DocuSign.com.</span><span class="sxs-lookup"><span data-stu-id="fe412-136">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="fe412-137">b.</span><span class="sxs-lookup"><span data-stu-id="fe412-137">b.</span></span> <span data-ttu-id="fe412-138">Na caixa de texto **Senha do Administrador**, digite a senha dessa conta.</span><span class="sxs-lookup"><span data-stu-id="fe412-138">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="fe412-139">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

7. <span data-ttu-id="fe412-140">No campo **Email de Notificação**, insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="fe412-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="fe412-141">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="fe412-141">Click **Save.**</span></span>

9. <span data-ttu-id="fe412-142">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o DocuSign.**</span><span class="sxs-lookup"><span data-stu-id="fe412-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

10. <span data-ttu-id="fe412-143">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="fe412-144">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do DocuSign em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="fe412-144">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="fe412-145">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="fe412-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="fe412-146">Para habilitar o serviço de provisionamento do Azure AD no DocuSign, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="fe412-146">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="fe412-147">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="fe412-147">Click **Save.**</span></span>

<span data-ttu-id="fe412-148">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao DocuSign na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="fe412-148">It starts the initial synchronization of any users and/or groups assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="fe412-149">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="fe412-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fe412-150">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="fe412-151">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="fe412-151">You can now create a test account.</span></span> <span data-ttu-id="fe412-152">Aguarde até 20 minutos para confirmar se a conta foi sincronizada com o DocuSign.</span><span class="sxs-lookup"><span data-stu-id="fe412-152">Wait for up to 20 minutes to verify that the account has been synchronized to DocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe412-153">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fe412-153">Additional resources</span></span>

* [<span data-ttu-id="fe412-154">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="fe412-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe412-155">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe412-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fe412-156">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="fe412-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)