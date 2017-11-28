---
title: "aplicativo aaaAn atribuído não aparece no painel de acesso Olá | Microsoft Docs"
description: "Solução de problemas que um aplicativo não é exibido no painel de acesso de saudação"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="2b5e3-103">Um aplicativo atribuído não aparece no painel de acesso Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="2b5e3-104">Olá painel de acesso é um portal baseado na web que permite que um usuário com um trabalho ou escola conta em aplicativos tooview e início baseado em nuvem do Azure Active Directory (AD do Azure) que Olá administrador do AD do Azure tem acesso-los ao.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="2b5e3-105">Esses aplicativos são configurados em nome de usuário de saudação no portal do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="2b5e3-106">aplicativo Hello deve ser configurado corretamente e atribuído toohello usuário ou grupo Olá é um membro de toosee aplicativo Olá Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="2b5e3-107">tipo Hello de aplicativos que um usuário pode ver se enquadram em Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="2b5e3-108">Aplicativos do Office 365</span><span class="sxs-lookup"><span data-stu-id="2b5e3-108">Office 365 Applications</span></span>

-   <span data-ttu-id="2b5e3-109">Aplicativos da Microsoft e de terceiros configurados com o SSO baseado em federação</span><span class="sxs-lookup"><span data-stu-id="2b5e3-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="2b5e3-110">Aplicativos de SSO baseadas em senhas</span><span class="sxs-lookup"><span data-stu-id="2b5e3-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="2b5e3-111">Aplicativos com soluções de SSO existentes</span><span class="sxs-lookup"><span data-stu-id="2b5e3-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="2b5e3-112">Geral emite toocheck primeiro</span><span class="sxs-lookup"><span data-stu-id="2b5e3-112">General issues toocheck first</span></span>

-   <span data-ttu-id="2b5e3-113">Se um aplicativo acabou de ser adicionado tooa usuário, tente toosign e sair novamente no painel de acesso do usuário Olá após toosee de alguns minutos se o aplicativo hello é adicionado.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="2b5e3-114">Se uma licença apenas foi removida de um usuário ou grupo Olá é que um membro deste pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo Olá toobe alterações feita.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="2b5e3-115">Permitir tempo extra antes de entrar no painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="2b5e3-116">Configuração de tooapplication relacionados de problemas</span><span class="sxs-lookup"><span data-stu-id="2b5e3-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="2b5e3-117">Um aplicativo pode não aparecer no Painel de Acesso de um usuário porque não está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="2b5e3-118">Abaixo estão algumas maneiras que você pode solucionar problemas de configuração de tooapplication relacionados de problemas:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="2b5e3-119">Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2b5e3-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="2b5e3-120">Logon único para um aplicativo da Galeria não como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2b5e3-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="2b5e3-121">Como tooconfigure uma senha única de logon no aplicativo para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b5e3-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="2b5e3-122">Como um único aplicativo de logon para um aplicativo da Galeria não tooconfigure uma senha</span><span class="sxs-lookup"><span data-stu-id="2b5e3-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="2b5e3-123">Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2b5e3-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="2b5e3-124">Todos os aplicativos na Galeria do Azure AD Olá habilitado com a funcionalidade do Enterprise Single Sign-On tem um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="2b5e3-125">Você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhadas.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="2b5e3-126">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2b5e3-127">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="2b5e3-128">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="2b5e3-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="2b5e3-129">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="2b5e3-130">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b5e3-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="2b5e3-131">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="2b5e3-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="2b5e3-132">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="2b5e3-133">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-134">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="2b5e3-135">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-136">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-137">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-138">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b5e3-139">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="2b5e3-140">Selecione aplicativo hello desejar tooconfigure para logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="2b5e3-141">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="2b5e3-142">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="2b5e3-143">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="2b5e3-144">Configurar logon único para um aplicativo da Galeria do AD do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="2b5e3-145">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-146">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-147">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-148">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-149">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-150">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b5e3-151">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-152">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-153">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-154">Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="2b5e3-155">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="2b5e3-156">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="2b5e3-157">aplicativo de hello tooconfigure como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="2b5e3-158">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="2b5e3-159">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, Olá URL de resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="2b5e3-160">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="2b5e3-161">**Opcional:** clique **Mostrar configurações de URL avançadas** se você quiser toosee Olá não obrigatórios valores.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="2b5e3-162">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="2b5e3-163">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2b5e3-164">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2b5e3-165">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-165">click **Add attribute**.</span></span> <span data-ttu-id="2b5e3-166">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2b5e3-167">clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-167">click **Save.**</span></span> <span data-ttu-id="2b5e3-168">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="2b5e3-169">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="2b5e3-170">Além disso, você tem Olá URLs de metadados e o certificado necessário toosetup SSO com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="2b5e3-171">Clique em **salvar** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="2b5e3-172">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="2b5e3-173">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="2b5e3-174">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-175">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-176">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-177">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-178">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-179">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b5e3-180">Se você não vir o aplicativo hello deseja tooshow aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-181">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-182">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-183">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="2b5e3-184">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="2b5e3-185">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="2b5e3-186">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="2b5e3-187">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2b5e3-188">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2b5e3-189">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-189">click **Add attribute**.</span></span> <span data-ttu-id="2b5e3-190">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2b5e3-191">clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-191">click **Save.**</span></span> <span data-ttu-id="2b5e3-192">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="2b5e3-193">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="2b5e3-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="2b5e3-194">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-195">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-196">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-197">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-198">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-199">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b5e3-200">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-201">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-202">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-203">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="2b5e3-204">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="2b5e3-205">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="2b5e3-206">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="2b5e3-207">Logon único para um aplicativo da Galeria não como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2b5e3-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="2b5e3-208">tooconfigure um aplicativo não galeria, é necessário toohave do Azure AD premium e aplicativo hello suporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="2b5e3-209">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2b5e3-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="2b5e3-210">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="2b5e3-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="2b5e3-211">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="2b5e3-212">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b5e3-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="2b5e3-213">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="2b5e3-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="2b5e3-214">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="2b5e3-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="2b5e3-215">tooconfigure logon único para um aplicativo que não está na Galeria do Azure AD hello, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-216">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-217">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-218">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-219">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-220">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b5e3-221">Clique em **aplicativo Galeria não** em Olá **adicionar seu próprio aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="2b5e3-222">Digite o nome de saudação do aplicativo hello em hello **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="2b5e3-223">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="2b5e3-224">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="2b5e3-225">Selecione **baseado no SAML logon** em Olá **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="2b5e3-226">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="2b5e3-227">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="2b5e3-228">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, digite Olá URL de resposta e Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="2b5e3-229">**Opcional:** tooconfigure aplicativo de hello como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="2b5e3-230">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="2b5e3-231">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2b5e3-232">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2b5e3-233">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-233">click **Add attribute**.</span></span> <span data-ttu-id="2b5e3-234">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2b5e3-235">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-235">Click **Save.**</span></span> <span data-ttu-id="2b5e3-236">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="2b5e3-237">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="2b5e3-238">Além disso, você tem URLs do AD do Azure e o certificado necessário para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="2b5e3-239">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="2b5e3-240">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-241">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-242">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-243">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-244">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-245">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2b5e3-246">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-247">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-248">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-249">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="2b5e3-250">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="2b5e3-251">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="2b5e3-252">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="2b5e3-253">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="2b5e3-254">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="2b5e3-255">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-255">click **Add attribute**.</span></span> <span data-ttu-id="2b5e3-256">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="2b5e3-257">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-257">Click **Save.**</span></span> <span data-ttu-id="2b5e3-258">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="2b5e3-259">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="2b5e3-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="2b5e3-260">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-261">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-262">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-263">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-264">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-265">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2b5e3-266">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-267">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-268">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-269">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="2b5e3-270">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="2b5e3-271">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="2b5e3-272">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="2b5e3-273">Como senha tooconfigure o logon único para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b5e3-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="2b5e3-274">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2b5e3-275">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="2b5e3-276">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b5e3-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="2b5e3-277">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="2b5e3-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="2b5e3-278">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-279">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="2b5e3-280">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-281">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-282">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-283">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b5e3-284">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="2b5e3-285">Selecione aplicativo hello desejar tooconfigure para logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="2b5e3-286">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="2b5e3-287">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="2b5e3-288">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2b5e3-289">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b5e3-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2b5e3-290">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-291">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-292">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-293">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-294">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-295">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="2b5e3-296">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-297">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-298">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-299">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2b5e3-300">[Atribuir usuários toohello aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="2b5e3-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="2b5e3-301">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2b5e3-302">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="2b5e3-303">Como senha tooconfigure o logon único para um aplicativo não Galeria</span><span class="sxs-lookup"><span data-stu-id="2b5e3-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="2b5e3-304">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="2b5e3-305">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="2b5e3-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="2b5e3-306">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b5e3-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="2b5e3-307">Adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="2b5e3-307">Add a non-gallery application</span></span>

<span data-ttu-id="2b5e3-308">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-309">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="2b5e3-310">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-311">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-312">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-313">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="2b5e3-314">clique em **Aplicativo inexistente na galeria.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="2b5e3-315">Insira o nome de saudação do seu aplicativo em Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="2b5e3-316">Selecione **Adicionar.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-316">Select **Add.**</span></span>

<span data-ttu-id="2b5e3-317">Após um curto período, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="2b5e3-318">Configurar o aplicativo hello de senha single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b5e3-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="2b5e3-319">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-320">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2b5e3-321">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-322">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-323">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-324">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="2b5e3-325">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-326">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="2b5e3-327">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-328">Modo de seleção Olá **com base em senha de logon.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="2b5e3-329">Digite hello **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="2b5e3-330">Isso é Olá URL onde os usuários digitarão seu nome de usuário e senha toosign em para.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="2b5e3-331">Certifique-se de campos de entrada hello são visíveis na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="2b5e3-332">[Atribuir usuários toohello aplicativo](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="2b5e3-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="2b5e3-333">Além disso, você também pode fornecer credenciais em nome de usuário de saudação selecionar linhas de saudação de usuários hello e clicando em **credenciais de atualização** e inserindo Olá nome de usuário e senha em nome dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="2b5e3-334">Caso contrário, os usuários ser solicitadas tooenter Olá credenciais si mesmos após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="2b5e3-335">Problemas relacionados tooassigning aplicativos toousers</span><span class="sxs-lookup"><span data-stu-id="2b5e3-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="2b5e3-336">Um usuário pode não estar vendo um aplicativo no respectivo painel de acesso porque eles não estão atribuídos toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="2b5e3-337">Abaixo estão algumas maneiras toocheck:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="2b5e3-338">Verifique se um usuário é atribuído toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="2b5e3-339">Como tooassign tooan aplicativo do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="2b5e3-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="2b5e3-340">Verifique se um usuário é atribuído a licença tooa relacionados ao aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="2b5e3-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="2b5e3-341">Como tooassign um usuário de tooa de licença</span><span class="sxs-lookup"><span data-stu-id="2b5e3-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="2b5e3-342">Verifique se um usuário é atribuído toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b5e3-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="2b5e3-343">toocheck toohello aplicativo, é atribuído a um usuário siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-344">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-345">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-346">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-347">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-348">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="2b5e3-349">**Pesquisa** para nome de saudação do aplicativo hello em questão.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="2b5e3-350">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="2b5e3-351">Verifique toosee se o usuário é atribuído a toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="2b5e3-352">Caso não siga etapas hello "como tooassign tooan aplicativo do usuário diretamente" toodo para.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="2b5e3-353">Como tooassign tooan aplicativo do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="2b5e3-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="2b5e3-354">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-355">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="2b5e3-356">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-357">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-358">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-359">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b5e3-360">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-361">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="2b5e3-362">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-363">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2b5e3-364">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2b5e3-365">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2b5e3-366">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="2b5e3-367">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="2b5e3-368">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="2b5e3-369">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="2b5e3-370">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="2b5e3-371">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="2b5e3-372">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="2b5e3-373">Verifique se um usuário está em uma licença relacionados ao aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="2b5e3-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="2b5e3-374">toocheck um usuário atribuído licenças, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-375">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-376">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-377">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-378">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-379">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-379">click **All users**.</span></span>

6.  <span data-ttu-id="2b5e3-380">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2b5e3-381">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="2b5e3-382">Se o usuário Olá é atribuído a licença do Office tooan isso habilitar tooappear de aplicativos do Office de terceiros primeiro em Olá painel de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="2b5e3-383">Como tooassign um usuário uma licença</span><span class="sxs-lookup"><span data-stu-id="2b5e3-383">How tooassign a user a license</span></span> 

<span data-ttu-id="2b5e3-384">tooassign um usuário de tooa de licença, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-385">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-386">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-387">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-388">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-389">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-389">click **All users**.</span></span>

6.  <span data-ttu-id="2b5e3-390">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2b5e3-391">Clique em **licenças** toosee quais licenças Olá atualmente atribuída ao usuário.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="2b5e3-392">Clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="2b5e3-393">Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="2b5e3-394">**Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="2b5e3-395">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2b5e3-396">Clique em Olá **atribuir** botão tooassign usuário de toothis essas licenças.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="2b5e3-397">Problemas relacionados tooassigning aplicativos toogroups</span><span class="sxs-lookup"><span data-stu-id="2b5e3-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="2b5e3-398">Um usuário pode ver um aplicativo no respectivo painel de acesso porque fazem parte de um grupo que tenha sido atribuído um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="2b5e3-399">Abaixo estão algumas maneiras toocheck:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="2b5e3-400">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2b5e3-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="2b5e3-401">Como tooassign tooa um aplicativo de grupo diretamente</span><span class="sxs-lookup"><span data-stu-id="2b5e3-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="2b5e3-402">Verifique se um usuário faz parte do grupo atribuído a licença tooa</span><span class="sxs-lookup"><span data-stu-id="2b5e3-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="2b5e3-403">Como tooassign um grupo de licenças tooa</span><span class="sxs-lookup"><span data-stu-id="2b5e3-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="2b5e3-404">Verificar as associações de grupo de um usuário</span><span class="sxs-lookup"><span data-stu-id="2b5e3-404">Check a user’s group memberships</span></span>

<span data-ttu-id="2b5e3-405">toocheck a associação do grupo, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-406">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-407">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-408">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-409">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-410">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-410">click **All users**.</span></span>

6.  <span data-ttu-id="2b5e3-411">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2b5e3-412">clique em **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-412">click **Groups**.</span></span>

8.  <span data-ttu-id="2b5e3-413">Verifique toosee se o usuário fizer parte de um aplicativo de toohello grupo atribuído.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="2b5e3-414">Se você desejar tooremove Olá usuário do grupo de saudação **clique linha hello** do grupo de saudação e selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="2b5e3-415">Como tooassign tooa um aplicativo de grupo diretamente</span><span class="sxs-lookup"><span data-stu-id="2b5e3-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="2b5e3-416">tooassign um ou mais grupos de aplicativo tooan diretamente, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-417">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="2b5e3-418">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-419">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-420">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-421">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2b5e3-422">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2b5e3-423">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="2b5e3-424">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b5e3-425">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2b5e3-426">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2b5e3-427">Tipo de saudação **nome completo do grupo** do grupo de saudação que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2b5e3-428">Passe o mouse sobre Olá **grupo** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="2b5e3-429">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello grupo seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="2b5e3-430">**Opcional:** se você gostaria que muito**adicionar mais de um grupo**, tipo em outro **nome completo do grupo** em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa e clique em tooadd de caixa de seleção Olá esse grupo toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="2b5e3-431">Quando você terminar de selecionar os grupos, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="2b5e3-432">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect toohello de tooassign uma função grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="2b5e3-433">Clique em Olá **atribuir** grupos selecionados do botão tooassign Olá aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="2b5e3-434">Após um curto período, os usuários Olá que você selecionou ser capaz de toolaunch esses aplicativos em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="2b5e3-435">Verifique se um usuário faz parte do grupo atribuído a licença tooa</span><span class="sxs-lookup"><span data-stu-id="2b5e3-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="2b5e3-436">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-437">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-438">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-439">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-440">Clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-440">click **All users**.</span></span>

6.  <span data-ttu-id="2b5e3-441">**Pesquisa** para usuário Olá que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2b5e3-442">clique em **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-442">click **Groups**.</span></span>

8.  <span data-ttu-id="2b5e3-443">Clique em linha de saudação de um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="2b5e3-444">Clique em **licenças** toosee qual grupo de licenças Olá atribuiu tooit.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="2b5e3-445">Se o grupo de saudação for atribuído a licença do Office tooan em que isso pode habilitar determinado tooappear de aplicativos do Office de terceiros primeiro Olá painel de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="2b5e3-446">Como tooassign um grupo de licenças tooa</span><span class="sxs-lookup"><span data-stu-id="2b5e3-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="2b5e3-447">tooassign um grupo de tooa de licença, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="2b5e3-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="2b5e3-448">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="2b5e3-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b5e3-449">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b5e3-450">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b5e3-451">Clique em **usuários e grupos** no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2b5e3-452">clique em **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-452">click **All groups**.</span></span>

6.  <span data-ttu-id="2b5e3-453">**Pesquisa** para grupo de saudação que lhe interessam e **clique linha hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2b5e3-454">Clique em **licenças** toosee qual grupo de licenças Olá atualmente tem atribuída.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="2b5e3-455">Clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="2b5e3-456">Selecione **um ou mais produtos** da lista de saudação de produtos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="2b5e3-457">**Opcional** clique Olá **opções atribuição** item toogranularly atribuir produtos.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="2b5e3-458">Clique em **OK** quando isso for concluído.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2b5e3-459">Clique em Olá **atribuir** botão tooassign grupo de toothis essas licenças.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="2b5e3-460">Isso pode levar algum tempo, dependendo do tamanho de saudação e a complexidade do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="2b5e3-461">toodo isso mais rapidamente, considere temporariamente atribuir uma licença toohello usuário diretamente.</span><span class="sxs-lookup"><span data-stu-id="2b5e3-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="2b5e3-462">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b5e3-462">Next steps</span></span>
[<span data-ttu-id="2b5e3-463">Adicionar novo tooAzure de usuários do Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b5e3-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

