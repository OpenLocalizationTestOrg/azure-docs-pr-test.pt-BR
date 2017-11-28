---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="b64c1-103">Tutorial: configurar o Workplace by Facebook para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="b64c1-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="b64c1-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Workplace by Facebook e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b64c1-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b64c1-105">Prerequisites</span></span>

<span data-ttu-id="b64c1-106">Para configurar a integração do Azure AD com o Workplace by Facebook, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b64c1-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="b64c1-107">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b64c1-107">An Azure AD subscription</span></span>
- <span data-ttu-id="b64c1-108">Uma assinatura do Workplace by Facebook habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="b64c1-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b64c1-109">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b64c1-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b64c1-110">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b64c1-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b64c1-111">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b64c1-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b64c1-112">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b64c1-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="b64c1-113">Atribuição de usuários ao Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="b64c1-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="b64c1-114">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="b64c1-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b64c1-115">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="b64c1-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b64c1-116">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="b64c1-117">Depois de decidir, atribua esses usuários ao seu aplicativo Workplace by Facebook seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="b64c1-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="b64c1-118">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="b64c1-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="b64c1-119">Dicas importantes para atribuir usuários ao Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="b64c1-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="b64c1-120">Recomendamos a atribuição de um único usuário do Azure AD ao Workplace by Facebook para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b64c1-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="b64c1-121">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b64c1-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b64c1-122">Ao atribuir um usuário ao Workplace by Facebook, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="b64c1-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="b64c1-123">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b64c1-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="b64c1-124">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="b64c1-124">Enable User Provisioning</span></span>

<span data-ttu-id="b64c1-125">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Workplace by Facebook e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Workplace by Facebook, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b64c1-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b64c1-126">Você também pode optar por habilitar o Logon Único baseado em SAML no Workplace by Facebook, seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b64c1-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b64c1-127">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="b64c1-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="b64c1-128">Para configurar o provisionamento de conta de usuário para o Workplace by Facebook no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b64c1-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="b64c1-129">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="b64c1-130">O Azure AD dá suporte à capacidade de sincronizar automaticamente os detalhes da conta de usuários atribuídos ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="b64c1-131">Essa sincronização automática permite que o Workplace by Facebook obtenha os dados necessários para autorizar o acesso aos usuários, antes que eles tentem se conectar pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="b64c1-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="b64c1-132">Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b64c1-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="b64c1-133">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory** > **Aplicativos Empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b64c1-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="b64c1-134">Se você já tiver configurado o Workplace by Facebook para logon único, pesquise a instância do Workplace by Facebook usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b64c1-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="b64c1-135">Caso contrário, selecione **Adicionar** e pesquise **Workplace by Facebook** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b64c1-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="b64c1-136">Selecione o Workplace by Facebook nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b64c1-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b64c1-137">Selecione a instância do Workplace by Facebook e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="b64c1-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b64c1-138">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="b64c1-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b64c1-140">Na seção **Credenciais de Administrador**, insira o Token Secreto e a URL de Locatário do administrador do Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="b64c1-141">No Portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD possa se conectar ao aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="b64c1-142">Se a conexão falhar, verifique se sua conta do Workplace by Facebook tem permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="b64c1-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="b64c1-143">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="b64c1-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="b64c1-144">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b64c1-144">Click **Save.**</span></span>

9. <span data-ttu-id="b64c1-145">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Workplace by Facebook.**</span><span class="sxs-lookup"><span data-stu-id="b64c1-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="b64c1-146">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="b64c1-147">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Workplace by Facebook em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="b64c1-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="b64c1-148">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="b64c1-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="b64c1-149">Para habilitar o serviço de provisionamento do Azure AD no Workplace by Facebook, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="b64c1-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="b64c1-150">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b64c1-150">Click **Save.**</span></span>

<span data-ttu-id="b64c1-151">Para obter mais informações sobre como configurar o provisionamento automático, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="b64c1-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="b64c1-152">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b64c1-152">You can now create a test account.</span></span> <span data-ttu-id="b64c1-153">Aguarde até 20 minutos para verificar se a conta foi sincronizada com o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="b64c1-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b64c1-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b64c1-154">Additional resources</span></span>

* [<span data-ttu-id="b64c1-155">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="b64c1-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b64c1-156">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b64c1-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b64c1-157">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="b64c1-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

