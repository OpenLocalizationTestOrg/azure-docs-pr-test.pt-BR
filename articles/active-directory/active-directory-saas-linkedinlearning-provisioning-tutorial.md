---
title: "Tutorial: Configurar o LinkedIn Learning para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar e desprovisionar automaticamente contas de usuário no LinkedIn Learning."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5eb2b1594eedb2a135d7b8cd501a33d8264e136b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a><span data-ttu-id="f0806-103">Tutorial: Configurar o LinkedIn Learning para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="f0806-103">Tutorial: Configuring LinkedIn Learning for Automatic User Provisioning</span></span>


<span data-ttu-id="f0806-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no LinkedIn Learning e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="f0806-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Learning and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Learning.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f0806-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0806-105">Prerequisites</span></span>

<span data-ttu-id="f0806-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f0806-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f0806-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0806-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="f0806-108">Um locatário do LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f0806-108">A LinkedIn Learning tenant</span></span> 
*   <span data-ttu-id="f0806-109">Uma conta de administrador no LinkedIn Learning com acesso ao Centro de Contas do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="f0806-109">An administrator account in LinkedIn Learning with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="f0806-110">O Azure Active Directory integra-se com o LinkedIn Learning usando o protocolo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="f0806-110">Azure Active Directory integrates with LinkedIn Learning using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-learning"></a><span data-ttu-id="f0806-111">Atribuir usuários ao LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f0806-111">Assigning users to LinkedIn Learning</span></span>

<span data-ttu-id="f0806-112">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="f0806-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f0806-113">No contexto do provisionamento automático de conta de usuário, somente os usuários e grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="f0806-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="f0806-114">Antes de configurar e habilitar o serviço de provisionamento, você precisará decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="f0806-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Learning.</span></span> <span data-ttu-id="f0806-115">Depois de decidir, atribua esses usuários ao LinkedIn Learning seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="f0806-115">Once decided, you can assign these users to LinkedIn Learning by following the instructions here:</span></span>

[<span data-ttu-id="f0806-116">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="f0806-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-learning"></a><span data-ttu-id="f0806-117">Dicas importantes para atribuir usuários ao LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f0806-117">Important tips for assigning users to LinkedIn Learning</span></span>

*   <span data-ttu-id="f0806-118">Recomendamos a atribuição de um único usuário do Azure AD ao LinkedIn Learning para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="f0806-118">It is recommended that a single Azure AD user be assigned to LinkedIn Learning to test the provisioning configuration.</span></span> <span data-ttu-id="f0806-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f0806-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f0806-120">Ao atribuir um usuário ao LinkedIn Learning, selecione a função **Usuário** na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="f0806-120">When assigning a user to LinkedIn Learning, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="f0806-121">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="f0806-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-learning"></a><span data-ttu-id="f0806-122">Como configurar o provisionamento de usuários no LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f0806-122">Configuring user provisioning to LinkedIn Learning</span></span>

<span data-ttu-id="f0806-123">Esta seção orienta você pela conexão do Azure AD à API de provisionamento de conta de usuário do SCIM do LinkedIn Learning e também pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no LinkedIn Learning com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0806-123">This section guides you through connecting your Azure AD to LinkedIn Learning's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Learning based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="f0806-124">Você também pode optar por habilitar o logon único baseado em SAML para o LinkedIn Learning seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0806-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Learning, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f0806-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="f0806-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-learning-in-azure-ad"></a><span data-ttu-id="f0806-126">Para configurar o provisionamento de conta de usuário automático para o LinkedIn Learning no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f0806-126">To configure automatic user account provisioning to LinkedIn Learning in Azure AD:</span></span>


<span data-ttu-id="f0806-127">A primeira etapa é recuperar o token de acesso do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f0806-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="f0806-128">Se você for um administrador corporativo, você poderá provisionar um token de acesso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f0806-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="f0806-129">No seu centro de contas, vá para **Configurações &gt; Configurações Globais** e abra o painel **Instalação do SCIM**.</span><span class="sxs-lookup"><span data-stu-id="f0806-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="f0806-130">Se você estiver acessando o centro de contas diretamente em vez de fazê-lo por meio de um link, você poderá alcançá-lo usando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0806-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="f0806-131">Entre no Centro de Contas.</span><span class="sxs-lookup"><span data-stu-id="f0806-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="f0806-132">Selecione **Administrador &gt; Configurações de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="f0806-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="f0806-133">Clique em **Integrações Avançadas** na barra lateral esquerda.</span><span class="sxs-lookup"><span data-stu-id="f0806-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="f0806-134">Você será direcionado para o Centro de Contas.</span><span class="sxs-lookup"><span data-stu-id="f0806-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="f0806-135">Clique em **+ Adicionar a nova configuração de SCIM** e siga o procedimento preenchendo cada campo.</span><span class="sxs-lookup"><span data-stu-id="f0806-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="f0806-136">Quando a atribuição automática de licenças não está habilitada, isso significa que somente os dados de usuário estão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="f0806-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Provisionamento do LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="f0806-138">Quando a atribuição automática de licenças estiver habilitada, você precisa anotar o tipo de licença e a instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0806-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="f0806-139">Licenças são atribuídas por ordem de chegada, até que todas as licenças tenham sido utilizadas.</span><span class="sxs-lookup"><span data-stu-id="f0806-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Provisionamento do LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="f0806-141">Clique em **Gerar token**.</span><span class="sxs-lookup"><span data-stu-id="f0806-141">Click **Generate token**.</span></span> <span data-ttu-id="f0806-142">Você deve ver o token de acesso ser exibido sob o campo **Token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="f0806-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="f0806-143">Salve seu token de acesso para a área de transferência ou o computador antes de sair da página.</span><span class="sxs-lookup"><span data-stu-id="f0806-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="f0806-144">Em seguida, entre no [Portal do Azure](https://portal.azure.com) e navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0806-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="f0806-145">Se você já tiver configurado o LinkedIn Learning para logon único, pesquise por sua instância do LinkedIn Learning usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f0806-145">If you have already configured LinkedIn Learning for single sign-on, search for your instance of LinkedIn Learning using the search field.</span></span> <span data-ttu-id="f0806-146">Caso contrário, selecione **Adicionar** e pesquise por **LinkedIn Learning** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f0806-146">Otherwise, select **Add** and search for **LinkedIn Learning** in the application gallery.</span></span> <span data-ttu-id="f0806-147">Selecione o LinkedIn Learning nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f0806-147">Select LinkedIn Learning from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="f0806-148">Selecione sua instância do LinkedIn Learning e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="f0806-148">Select your instance of LinkedIn Learning, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="f0806-149">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="f0806-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Provisionamento do LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="f0806-151">Preencha os campos a seguir em **Credenciais de Administrador**:</span><span class="sxs-lookup"><span data-stu-id="f0806-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="f0806-152">Na **URL do Locatário**, digite https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="f0806-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="f0806-153">No campo **Segredo do Token**, insira o token de acesso gerado na etapa 1 e clique em **Testar Conexão**.</span><span class="sxs-lookup"><span data-stu-id="f0806-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="f0806-154">Você verá uma notificação de êxito no lado do superior direito do seu Portal.</span><span class="sxs-lookup"><span data-stu-id="f0806-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="f0806-155">Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="f0806-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="f0806-156">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f0806-156">Click **Save**.</span></span> 

14) <span data-ttu-id="f0806-157">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário e grupo que serão sincronizados do Azure AD para o LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="f0806-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Learning.</span></span> <span data-ttu-id="f0806-158">Observe que os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário e grupos no LinkedIn Learning para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="f0806-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Learning for update operations.</span></span> <span data-ttu-id="f0806-159">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="f0806-159">Select the Save button to commit any changes.</span></span>

![Provisionamento do LinkedIn Learning](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="f0806-161">Para habilitar o serviço de provisionamento do Azure AD para o LinkedIn Learning, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="f0806-161">To enable the Azure AD provisioning service for LinkedIn Learning, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="f0806-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f0806-162">Click **Save**.</span></span> 

<span data-ttu-id="f0806-163">Isso iniciará a sincronização inicial de todos os usuários e/ou grupos atribuídos ao LinkedIn Learning na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="f0806-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Learning in the Users and Groups section.</span></span> <span data-ttu-id="f0806-164">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="f0806-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="f0806-165">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="f0806-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Learning app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f0806-166">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f0806-166">Additional Resources</span></span>

* [<span data-ttu-id="f0806-167">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="f0806-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f0806-168">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0806-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
