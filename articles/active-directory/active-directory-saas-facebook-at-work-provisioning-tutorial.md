---
title: "Tutorial: configurar o Workplace by Facebook para provisionamento de usuário | Microsoft Docs"
description: "Saiba como provisionar e desprovisionar automaticamente contas de usuário do Azure AD para o Workplace by Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: a347eedbf5511dc83e1bc7721667441cfb87cb59
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="4f748-103">Tutorial: configurar o Workplace by Facebook para provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="4f748-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="4f748-104">Este tutorial mostra as etapas necessárias para provisionar e cancelar o provisionamento de contas de usuário automaticamente do Azure AD (Azure Active Directory) para o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-104">This tutorial shows you the steps necessary to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f748-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4f748-105">Prerequisites</span></span>

<span data-ttu-id="4f748-106">Para configurar a integração do Azure AD com o Workplace by Facebook, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4f748-106">To configure Azure AD integration with Workplace by Facebook, you need the following:</span></span>

- <span data-ttu-id="4f748-107">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4f748-107">An Azure AD subscription</span></span>
- <span data-ttu-id="4f748-108">Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="4f748-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4f748-109">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4f748-109">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4f748-110">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4f748-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f748-111">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma [oferta de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f748-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-workplace-by-facebook"></a><span data-ttu-id="4f748-112">Atribuir usuários ao Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4f748-112">Assign users to Workplace by Facebook</span></span>

<span data-ttu-id="4f748-113">O Azure AD usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="4f748-113">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4f748-114">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram atribuídos a um aplicativo no Azure AD são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="4f748-114">In the context of automatic user account provisioning, only the users and groups that have been assigned to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="4f748-115">Antes de configurar e habilitar o serviço de provisionamento, decida quais usuários e grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-115">Before configuring and enabling the provisioning service, decide what users and groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="4f748-116">Depois disso, você pode atribuir esses usuários ao aplicativo Workplace by Facebook seguindo a instruções em [Atribuir um usuário ou grupo a um aplicativo empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="4f748-116">You can then assign these users to your Workplace by Facebook app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="4f748-117">Teste a configuração de provisionamento atribuindo um único usuário do Azure AD ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-117">Test the provisioning configuration by assigning a single Azure AD user to Workplace by Facebook.</span></span> <span data-ttu-id="4f748-118">Atribua usuários e grupos adicionais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="4f748-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="4f748-119">Ao atribuir um usuário ao Workplace by Facebook, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="4f748-119">When you assign a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="4f748-120">A função de Acesso Padrão não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="4f748-120">The Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4f748-121">Habilitar o provisionamento automatizado de usuários</span><span class="sxs-lookup"><span data-stu-id="4f748-121">Enable automated user provisioning</span></span>

<span data-ttu-id="4f748-122">Esta seção orienta você sobre como conectar o Azure AD à API de provisionamento de conta de usuário do Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-122">This section guides you through connecting your Azure AD to the user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="4f748-123">Você também aprenderá a configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-123">You also learn how to configure the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="4f748-124">Isso se baseia na atribuição de usuários e grupos no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f748-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4f748-125">Você também pode optar por habilitar o SSO baseado em SAML para o Workplace by Facebook, seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f748-125">You can also choose to enabled SAML-based SSO for Workplace by Facebook, by following the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f748-126">O SSO pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="4f748-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="4f748-127">Configurar o provisionamento de conta de usuário para o Workplace by Facebook no Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f748-127">Configure user account provisioning to Workplace by Facebook in Azure AD</span></span>

<span data-ttu-id="4f748-128">O Azure AD dá suporte à capacidade de sincronizar automaticamente os detalhes da conta de usuários atribuídos ao Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-128">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="4f748-129">Essa sincronização automática permite que o Workplace by Facebook obtenha os dados necessários para autorizar o acesso aos usuários, antes que eles tentem se conectar pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="4f748-129">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="4f748-130">Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f748-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="4f748-131">No [Portal do Azure](https://portal.azure.com), selecione **Azure Active Directory** > **Aplicativos Empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4f748-131">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="4f748-132">Se você já tiver configurado o Workplace by Facebook para SSO, pesquise a instância do Workplace by Facebook usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="4f748-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using the search field.</span></span> <span data-ttu-id="4f748-133">Caso contrário, selecione **Adicionar** e pesquise **Workplace by Facebook** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4f748-133">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="4f748-134">Selecione o **Workplace by Facebook** nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4f748-134">Select **Workplace by Facebook** from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="4f748-135">Selecione a instância do Workplace by Facebook e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="4f748-135">Select your instance of Workplace by Facebook, and then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="4f748-136">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="4f748-136">Set **Provisioning Mode** to **Automatic**.</span></span> 

    ![Captura de tela das opções de provisionamento do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="4f748-138">Na seção **Credenciais de Administrador**, insira o **Token Secreto** e a **URL de Locatário** do administrador do Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-138">Under the **Admin Credentials** section, enter the **Secret Token** and the **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="4f748-139">No Portal do Azure, selecione **Testar conexão** para garantir que o Azure AD possa se conectar ao aplicativo Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-139">In the Azure portal, select **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="4f748-140">Se a conexão falhar, verifique se sua conta do Workplace by Facebook tem permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="4f748-140">If the connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="4f748-141">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="4f748-141">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the check box.</span></span>

8. <span data-ttu-id="4f748-142">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4f748-142">Select **Save**.</span></span>

9. <span data-ttu-id="4f748-143">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="4f748-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.</span></span>

10. <span data-ttu-id="4f748-144">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="4f748-145">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Workplace by Facebook em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="4f748-145">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="4f748-146">Para confirmar as alterações, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4f748-146">To commit any changes, select **Save**.</span></span>

11. <span data-ttu-id="4f748-147">Para habilitar o serviço de provisionamento do Azure AD no Workplace by Facebook, na seção **Configurações,** altere o **Status de provisionamento** para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="4f748-147">To enable the Azure AD provisioning service for Workplace by Facebook, in the **Settings** section, change the **Provisioning Status** to **On**.</span></span>

12. <span data-ttu-id="4f748-148">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4f748-148">Select **Save**.</span></span>

<span data-ttu-id="4f748-149">Para obter mais informações sobre como configurar o provisionamento automático, consulte [a documentação do Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="4f748-149">For more information on how to configure automatic provisioning, see [the Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="4f748-150">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="4f748-150">You can now create a test account.</span></span> <span data-ttu-id="4f748-151">Aguarde até 20 minutos para verificar se a conta foi sincronizada com o Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4f748-151">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f748-152">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4f748-152">Additional resources</span></span>

* [<span data-ttu-id="4f748-153">Gerenciamento do provisionamento de conta de usuário para aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="4f748-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f748-154">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f748-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4f748-155">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="4f748-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

