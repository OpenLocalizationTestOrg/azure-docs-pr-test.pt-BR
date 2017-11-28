---
title: aaaHow tooconfigure federado SSO para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Logon único para um existente Galeria do Azure AD aplicativo e como usar tutoriais tooget ir rapidamente como federado tooconfigure"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="ce08a-103">Logon único para um aplicativo da Galeria do Azure AD como federado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="ce08a-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="ce08a-104">Todos os aplicativos na Galeria de saudação do AD do Azure habilitado com o recurso de logon único corporativo tem um tutorial passo a passo disponível.</span><span class="sxs-lookup"><span data-stu-id="ce08a-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="ce08a-105">Você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obter orientações passo a passo detalhadas.</span><span class="sxs-lookup"><span data-stu-id="ce08a-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="ce08a-106">Visão geral das etapas necessárias</span><span class="sxs-lookup"><span data-stu-id="ce08a-106">Overview of steps required</span></span>
<span data-ttu-id="ce08a-107">tooconfigure um aplicativo da Galeria do AD do Azure Olá você precisa:</span><span class="sxs-lookup"><span data-stu-id="ce08a-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ce08a-108">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="ce08a-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="ce08a-109">Configurar valores de metadados do aplicativo hello no AD do Azure (logon de URL, identificador, a URL de resposta)</span><span class="sxs-lookup"><span data-stu-id="ce08a-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="ce08a-110">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="ce08a-111">Recuperar certificado e metadados Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce08a-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="ce08a-112">Configurar valores de metadados do AD do Azure no aplicativo hello (logon URL, o emissor, o URL de Logout e certificado)</span><span class="sxs-lookup"><span data-stu-id="ce08a-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="ce08a-113">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ce08a-114">Adicionar um aplicativo da Galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="ce08a-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ce08a-115">tooadd um aplicativo hello Galeria do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce08a-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ce08a-116">Olá abrir [Portal do Azure](https://portal.azure.com) e entre como um **Administrador Global** ou **Co-administrador**</span><span class="sxs-lookup"><span data-stu-id="ce08a-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ce08a-117">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ce08a-118">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="ce08a-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ce08a-119">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ce08a-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ce08a-120">Clique em Olá **adicionar** botão no canto superior direito Olá Olá **aplicativos empresariais** folha.</span><span class="sxs-lookup"><span data-stu-id="ce08a-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="ce08a-121">Em Olá **Insira um nome** caixa de texto de saudação **adicionar da Galeria Olá** seção, digite o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="ce08a-122">Selecione aplicativo hello desejar tooconfigure para logon único.</span><span class="sxs-lookup"><span data-stu-id="ce08a-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="ce08a-123">Antes de adicionar o aplicativo hello, você pode alterar seu nome de saudação **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ce08a-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="ce08a-124">Clique em **adicionar** botão, o aplicativo de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce08a-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="ce08a-125">Após um curto período de tempo, você deve ser folha de configuração do aplicativo do toosee capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ce08a-126">Configurar logon único para um aplicativo da Galeria do AD do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="ce08a-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ce08a-127">tooconfigure logon único para um aplicativo, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce08a-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ce08a-128">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="ce08a-129">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ce08a-130">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="ce08a-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ce08a-131">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ce08a-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ce08a-132">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce08a-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ce08a-133">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ce08a-134">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ce08a-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ce08a-135">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ce08a-136">Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ce08a-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="ce08a-137">Digite os valores hello necessárias nas **URLs e domínio.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="ce08a-138">Você deve obter esses valores do fornecedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="ce08a-139">aplicativo de hello tooconfigure como SSO iniciado por SP, Olá logon na URL é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ce08a-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="ce08a-140">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ce08a-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="ce08a-141">aplicativo de hello tooconfigure como iniciado pelo IdP SSO, Olá URL de resposta é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ce08a-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="ce08a-142">Para alguns aplicativos, Olá identificador também é um valor obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ce08a-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="ce08a-143">**Opcional:** clique **Mostrar configurações de URL avançadas** se você quiser toosee Olá não obrigatórios valores.</span><span class="sxs-lookup"><span data-stu-id="ce08a-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="ce08a-144">Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ce08a-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="ce08a-145">**Opcional:** clique **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="ce08a-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="ce08a-146">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="ce08a-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="ce08a-147">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-147">click **Add attribute**.</span></span> <span data-ttu-id="ce08a-148">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="ce08a-149">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-149">Click **Save.**</span></span> <span data-ttu-id="ce08a-150">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="ce08a-151">Clique em **configurar &lt;nome do aplicativo&gt;**  tooaccess documentação sobre como tooconfigure logon único no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="ce08a-152">Além disso, você tem Olá URLs de metadados e o certificado necessário toosetup SSO com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="ce08a-153">Clique em **salvar** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="ce08a-154">Atribua usuários toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce08a-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="ce08a-155">Selecione o identificador de usuário e adicionar usuário atributos toobe enviado toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="ce08a-156">tooselect Olá identificador de usuário ou adicione atributos de usuário, execute as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce08a-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="ce08a-157">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ce08a-158">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ce08a-159">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="ce08a-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ce08a-160">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ce08a-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ce08a-161">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce08a-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ce08a-162">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ce08a-163">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="ce08a-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ce08a-164">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ce08a-165">Em Olá **atributos de usuário** seção, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="ce08a-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="ce08a-166">Olá opção selecionada deve toomatch Olá esperado valor no usuário de saudação do hello aplicativo tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="ce08a-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="ce08a-167">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="ce08a-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="ce08a-168">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="ce08a-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="ce08a-169">tooadd atributos de usuário, clique em **exibir e editar todos os outros atributos de usuário** tooedit Olá atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.</span><span class="sxs-lookup"><span data-stu-id="ce08a-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="ce08a-170">um atributo de tooadd:</span><span class="sxs-lookup"><span data-stu-id="ce08a-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="ce08a-171">clique em **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-171">click **Add attribute**.</span></span> <span data-ttu-id="ce08a-172">Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="ce08a-173">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-173">Click **Save**.</span></span> <span data-ttu-id="ce08a-174">Você verá um novo atributo Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="ce08a-175">Download de metadados do AD do Azure hello ou certificado</span><span class="sxs-lookup"><span data-stu-id="ce08a-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="ce08a-176">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce08a-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="ce08a-177">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ce08a-178">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ce08a-179">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="ce08a-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ce08a-180">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ce08a-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ce08a-181">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce08a-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="ce08a-182">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="ce08a-183">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="ce08a-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ce08a-184">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ce08a-185">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="ce08a-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="ce08a-186">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="ce08a-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="ce08a-187">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="ce08a-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="ce08a-188">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="ce08a-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="ce08a-189">Atribuir usuários toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-189">Assign users toohello application</span></span>

<span data-ttu-id="ce08a-190">tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce08a-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ce08a-191">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ce08a-192">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ce08a-193">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="ce08a-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ce08a-194">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ce08a-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ce08a-195">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce08a-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ce08a-196">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="ce08a-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ce08a-197">Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.</span><span class="sxs-lookup"><span data-stu-id="ce08a-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ce08a-198">Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce08a-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ce08a-199">Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="ce08a-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ce08a-200">Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.</span><span class="sxs-lookup"><span data-stu-id="ce08a-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ce08a-201">Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ce08a-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ce08a-202">Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="ce08a-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ce08a-203">Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ce08a-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ce08a-204">**Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ce08a-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ce08a-205">Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce08a-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ce08a-206">**Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="ce08a-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ce08a-207">Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.</span><span class="sxs-lookup"><span data-stu-id="ce08a-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="ce08a-208">Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce08a-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="ce08a-209">Personalizando Olá SAML declarações enviadas tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="ce08a-210">toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ce08a-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce08a-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce08a-211">Next steps</span></span>
[<span data-ttu-id="ce08a-212">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce08a-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



