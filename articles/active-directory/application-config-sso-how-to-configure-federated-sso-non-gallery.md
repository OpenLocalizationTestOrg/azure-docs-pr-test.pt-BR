---
title: "aaaHow tooconfigure federado SSO para um aplicativo não Galeria | Microsoft Docs"
description: "Logon único para um aplicativo não Galeria personalizado que você deseja toointegrate com o Azure AD como federado tooconfigure"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="87f90-103">Logon único para um aplicativo da Galeria não como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="87f90-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="87f90-104">tooconfigure um aplicativo não galeria, é necessário toohave do Azure AD premium e aplicativo hello suporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="87f90-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="87f90-105">Para obter mais informações sobre as versões do Azure AD, visite [Preços do Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="87f90-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="87f90-106">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="87f90-106">Overview of steps required</span></span>
<span data-ttu-id="87f90-107">Abaixo está uma visão geral de alto nível da saudação etapas necessárias tooconfigure federado logon único para uma galeria-não (por exemplo, personalizado) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87f90-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="87f90-108">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="87f90-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="87f90-109">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="87f90-110">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="87f90-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="87f90-111">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="87f90-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="87f90-112">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="87f90-113">Configurando aplicativos único logon toonon-Galeria</span><span class="sxs-lookup"><span data-stu-id="87f90-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="87f90-114">tooconfigure logon único para um aplicativo que não está na Galeria do Azure AD hello, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="87f90-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="87f90-115">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="87f90-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="87f90-116">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87f90-117">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="87f90-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87f90-118">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="87f90-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87f90-119">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="87f90-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="87f90-120">Clique em **aplicativo Galeria não** em Olá **adicionar seu próprio aplicativo** seção</span><span class="sxs-lookup"><span data-stu-id="87f90-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="87f90-121">Digite o nome de saudação do aplicativo hello em hello **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="87f90-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="87f90-122">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="87f90-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="87f90-123">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="87f90-124">Selecione **baseado no SAML logon** em Olá **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87f90-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="87f90-125">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="87f90-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="87f90-126">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="87f90-127">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, digite Olá URL de resposta e Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="87f90-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="87f90-128">**Opcional:** tooconfigure aplicativo de hello como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="87f90-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="87f90-129">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87f90-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="87f90-130">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="87f90-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="87f90-131">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="87f90-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="87f90-132">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="87f90-132">click **Add attribute**.</span></span> <span data-ttu-id="87f90-133">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="87f90-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="87f90-134">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="87f90-134">Click **Save.**</span></span> <span data-ttu-id="87f90-135">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="87f90-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="87f90-136">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="87f90-137">Além disso, você tem URLs do AD do Azure e o certificado necessário para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="87f90-138">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87f90-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="87f90-139">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="87f90-140">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="87f90-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="87f90-141">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="87f90-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="87f90-142">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87f90-143">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="87f90-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87f90-144">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="87f90-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87f90-145">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="87f90-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="87f90-146">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="87f90-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="87f90-147">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="87f90-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="87f90-148">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87f90-149">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87f90-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="87f90-150">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="87f90-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="87f90-151">[! Observação} AD do Azure Selecionar formato Olá Olá NameID identificador do atributo (usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="87f90-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="87f90-152">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="87f90-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="87f90-153">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="87f90-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="87f90-154">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="87f90-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="87f90-155">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="87f90-155">click **Add attribute**.</span></span> <span data-ttu-id="87f90-156">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="87f90-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="87f90-157">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="87f90-157">Click **Save.**</span></span> <span data-ttu-id="87f90-158">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="87f90-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="87f90-159">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="87f90-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="87f90-160">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="87f90-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="87f90-161">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="87f90-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="87f90-162">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87f90-163">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="87f90-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87f90-164">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="87f90-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87f90-165">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="87f90-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="87f90-166">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="87f90-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="87f90-167">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="87f90-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="87f90-168">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87f90-169">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="87f90-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="87f90-170">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="87f90-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="87f90-171">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="87f90-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="87f90-172">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="87f90-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="87f90-173">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-173">Assign users toohello application</span></span>

<span data-ttu-id="87f90-174">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="87f90-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="87f90-175">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="87f90-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87f90-176">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87f90-177">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="87f90-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87f90-178">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="87f90-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87f90-179">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="87f90-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="87f90-180">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="87f90-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="87f90-181">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="87f90-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="87f90-182">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="87f90-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87f90-183">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="87f90-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="87f90-184">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="87f90-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="87f90-185">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="87f90-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="87f90-186">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="87f90-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="87f90-187">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="87f90-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="87f90-188">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="87f90-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="87f90-189">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87f90-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="87f90-190">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="87f90-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="87f90-191">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="87f90-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="87f90-192">Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="87f90-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="87f90-193">Personalizando Olá SAML declarações enviadas tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="87f90-194">toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="87f90-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87f90-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87f90-195">Next steps</span></span>
[<span data-ttu-id="87f90-196">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="87f90-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
