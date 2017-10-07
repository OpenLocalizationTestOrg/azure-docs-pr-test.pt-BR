---
title: aaaProblem Configurando federado SSO para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Resolver alguns dos problemas comuns hello, você pode encontrar ao configurar federado único logon usando SAML para aplicativos que estão listados no hello Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="95de2-103">Problema ao configurar o logon único federado para um aplicativo na Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95de2-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="95de2-104">Se você encontrar um problema ao configurar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95de2-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="95de2-105">Verifique se que você tiver seguido todas as etapas de saudação tutorial Olá para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="95de2-106">Configuração do aplicativo hello, você tem embutido documentação sobre como tooconfigure Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95de2-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="95de2-107">Além disso, você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo de detalhes.</span><span class="sxs-lookup"><span data-stu-id="95de2-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="95de2-108">Não é possível adicionar outra instância do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="95de2-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="95de2-109">tooadd uma segunda instância de um aplicativo, você precisa toobe capaz de:</span><span class="sxs-lookup"><span data-stu-id="95de2-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="95de2-110">Configure um identificador exclusivo para a segunda instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="95de2-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="95de2-111">Você não será capaz de tooconfigure Olá mesmo identificador usado para a primeira instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="95de2-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="95de2-112">Configure um certificado diferente que Olá usada para Olá primeira instância.</span><span class="sxs-lookup"><span data-stu-id="95de2-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="95de2-113">Se hello aplicativo não oferece suporte a qualquer Olá acima.</span><span class="sxs-lookup"><span data-stu-id="95de2-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="95de2-114">Em seguida, não será capaz de tooconfigure uma segunda instância.</span><span class="sxs-lookup"><span data-stu-id="95de2-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="95de2-115">Não é possível adicionar Olá identificador ou Olá URL de resposta</span><span class="sxs-lookup"><span data-stu-id="95de2-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="95de2-116">Se você não for capaz de tooconfigure Olá identificador ou Olá URL de resposta, confirme Olá identificador e valores de URL de resposta correspondam de padrões de saudação pré-configurado para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="95de2-117">padrões de saudação tooknow pré-configurado para o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="95de2-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="95de2-118">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.** Vá toostep 7.</span><span class="sxs-lookup"><span data-stu-id="95de2-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="95de2-119">Se você já estiver na folha de configuração de aplicativo hello no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95de2-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="95de2-120">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95de2-121">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="95de2-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95de2-122">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="95de2-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95de2-123">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95de2-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="95de2-124">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="95de2-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="95de2-125">Selecione aplicativo hello deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="95de2-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="95de2-126">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95de2-127">Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="95de2-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="95de2-128">Vá toohello **identificador** ou **URL de resposta** textbox em Olá **seção URLs e de domínio.**</span><span class="sxs-lookup"><span data-stu-id="95de2-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="95de2-129">Há três maneiras tooknow padrões de saudação com suporte para o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="95de2-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="95de2-130">Na caixa de texto de saudação, verá Olá suporte para padrões como um espaço reservado *exemplo:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="95de2-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="95de2-131">Se não há suporte para o padrão de hello, você verá um ponto de exclamação vermelho quando você tentar o valor de saudação tooenter na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="95de2-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="95de2-132">Se você posicionar o mouse sobre o ponto de exclamação vermelho do hello, você veja os padrões de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="95de2-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="95de2-133">Tutorial de saudação para o aplicativo hello, você também pode obter informações sobre os padrões de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="95de2-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="95de2-134">Em Olá **logon único do AD do Azure de configurar** seção.</span><span class="sxs-lookup"><span data-stu-id="95de2-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="95de2-135">Etapa toohello vá para os valores de saudação configurado em Olá **domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="95de2-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="95de2-136">Se os valores de saudação não coincidem com os padrões de saudação configurados previamente no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95de2-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="95de2-137">Você pode:</span><span class="sxs-lookup"><span data-stu-id="95de2-137">You can:</span></span>

-   <span data-ttu-id="95de2-138">Trabalhar com hello aplicativo fornecedor tooget valores que correspondem a saudação padrão configurado previamente no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95de2-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="95de2-139">Ou, você pode contatar a equipe do AD do Azure em < aadapprequest@microsoft.com > ou deixar um comentário na atualização de Olá Olá tutorial toorequest dos padrões de saudação com suporte para o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="95de2-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="95de2-140">Onde definir o formato de ID (identificador de usuário) Olá</span><span class="sxs-lookup"><span data-stu-id="95de2-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="95de2-141">Não é o formato de ID (identificador de usuário) do hello tooselect capaz de AD do Azure envia toohello aplicativo em resposta Olá após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="95de2-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="95de2-142">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="95de2-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="95de2-143">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção Olá NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="95de2-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="95de2-144">Não é possível localizar a configuração de Olá Olá AD do Azure metadados toocomplete com o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="95de2-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="95de2-145">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="95de2-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="95de2-146">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="95de2-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="95de2-147">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95de2-148">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="95de2-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95de2-149">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="95de2-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95de2-150">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95de2-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="95de2-151">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="95de2-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="95de2-152">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="95de2-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="95de2-153">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="95de2-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95de2-154">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="95de2-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="95de2-155">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="95de2-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="95de2-156">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="95de2-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="95de2-157">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="95de2-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="95de2-158">Não sei como declarações SAML toocustomize enviado tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="95de2-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="95de2-159">toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="95de2-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95de2-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95de2-160">Next steps</span></span>
[<span data-ttu-id="95de2-161">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95de2-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
