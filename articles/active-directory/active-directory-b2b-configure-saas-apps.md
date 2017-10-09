---
title: "aplicativos de SaaS aaaConfigure para colaboração B2B no Active Directory do Azure | Microsoft Docs"
description: "Exemplos de código e do PowerShell para colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="1d8e8-103">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="1d8e8-104">A colaboração B2B do Azure Active Directory (Azure AD) funciona com a maioria dos aplicativos que se integra no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="1d8e8-105">Nesta seção, examinaremos as instruções de como configurar alguns aplicativos SaaS populares para usar com o B2B do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="1d8e8-106">Antes de examinarmos as instruções específicas do aplicativo, aqui estão algumas regras gerais:</span><span class="sxs-lookup"><span data-stu-id="1d8e8-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="1d8e8-107">Para a maioria dos aplicativos hello, configuração do usuário precisa toohappen manualmente.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="1d8e8-108">Ou seja, os usuários devem ser criados manualmente no aplicativo de saudação também.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="1d8e8-109">Para aplicativos que dão suporte a instalação automática, como o Dropbox, convites separados são criados nos aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="1d8e8-110">Os usuários deve ser tooaccept-se de que cada convite.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="1d8e8-111">Em atributos de usuário hello, toomitigate quaisquer problemas com o disco de perfil de usuário danificado (UDP) em usuários convidados, sempre defina **identificador de usuário** muito**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="1d8e8-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="1d8e8-112">Dropbox Business</span></span>

<span data-ttu-id="1d8e8-113">tooenable toosign de usuários usando sua conta de organização, você deve configurar manualmente Dropbox Business toouse AD do Azure como um provedor de identidade SAML Security Assertion Markup Language ().</span><span class="sxs-lookup"><span data-stu-id="1d8e8-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="1d8e8-114">Se Dropbox Business não foi configurado toodo assim, ele não é possível solicitar ou permitam toosign usuários usando AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="1d8e8-115">aplicativo de negócios Dropbox Olá tooadd no AD do Azure, selecione **aplicativos empresariais** Olá painel esquerdo e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![botão de "Adicionar" Hello na página de aplicativos da empresa de saudação](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="1d8e8-117">Em Olá **adicionar um aplicativo** janela, digite **dropbox** Olá caixa de pesquisa e, em seguida, selecione **Dropbox for Business** na lista de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Pesquise "dropbox" em Olá adicionar uma página de aplicativo](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="1d8e8-119">Em Olá **o logon único** página, selecione **o logon único** Olá painel esquerdo e, em seguida, digite **user.mail** em hello **identificador de usuário** caixa.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="1d8e8-120">(É definido como UPN por padrão.)</span><span class="sxs-lookup"><span data-stu-id="1d8e8-120">(It's set as UPN by default.)</span></span>

  ![Configurar o logon único para o aplicativo hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="1d8e8-122">toodownload Olá certificado toouse para configuração do Dropbox, selecione **configurar DropBox**e, em seguida, selecione **SAML Service URL de logon único** na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Baixando certificado Olá para configuração do Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="1d8e8-124">Entrar tooDropbox com hello URL de logon da saudação **o logon único** página.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![página Olá entrar no Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="1d8e8-126">No menu de saudação, selecione **Console de administração**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-126">On hello menu, select **Admin Console**.</span></span>

  ![link de "Console de administração" Hello no menu do Dropbox Olá](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="1d8e8-128">Em Olá **autenticação** caixa de diálogo, selecione **mais**, carregar certificado hello e, em seguida, em Olá **URL de logon** , digite a URL de saudação SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Olá link "Mais" na caixa de diálogo de autenticação Olá recolhido](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Olá "URL de entrada" no hello expandido a caixa de diálogo de autenticação](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="1d8e8-131">configuração de usuário automático de tooconfigure no hello portal do Azure, selecione **provisionamento** no painel esquerdo do hello, selecione **automático** em Olá **modo de provisionamento** caixa e, em seguida, selecione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configurar o provisionamento automático de usuário no portal do Azure de saudação](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="1d8e8-133">Depois usuários convidados ou membro foi configurados no aplicativo do Dropbox hello, eles recebem um convite separado do Dropbox.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="1d8e8-134">toouse logon único Dropbox, convidados devem aceitar o convite Olá clicando no link nele.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="1d8e8-135">Box</span><span class="sxs-lookup"><span data-stu-id="1d8e8-135">Box</span></span>
<span data-ttu-id="1d8e8-136">Você pode habilitar os usuários tooauthenticate caixa convidados com suas contas do AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="1d8e8-137">Neste procedimento, você deve carregar metadados tooBox.com.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="1d8e8-138">Adicione Olá caixa aplicativo de aplicativos corporativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="1d8e8-139">Configure o logon único Olá ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d8e8-139">Configure single sign-on in hello following order:</span></span>

  ![Configurar logon único do Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="1d8e8-141">a.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-141">a.</span></span> <span data-ttu-id="1d8e8-142">Em Olá **URL de logon** caixa, certifique-se de que o URL de entrada hello está definida corretamente para caixa em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="1d8e8-143">Essa URL é saudação do seu locatário Box.com.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="1d8e8-144">Você deve seguir a convenção de nomenclatura Olá *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="1d8e8-145">Olá **identificador** não se aplica a toothis aplicativo, mas ela ainda aparecerá como um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="1d8e8-146">b.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-146">b.</span></span> <span data-ttu-id="1d8e8-147">Em Olá **identificador de usuário** , digite **user.mail** (para o SSO para contas de convidado).</span><span class="sxs-lookup"><span data-stu-id="1d8e8-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="1d8e8-148">c.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-148">c.</span></span> <span data-ttu-id="1d8e8-149">Em **Certificado de Assinatura de SAML**, clique em **Criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="1d8e8-150">d.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-150">d.</span></span> <span data-ttu-id="1d8e8-151">toobegin configurar seu locatário de Box.com toouse AD do Azure como um provedor de identidade, baixe o arquivo de metadados de saudação e salve-a como unidade local tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="1d8e8-152">e.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-152">e.</span></span> <span data-ttu-id="1d8e8-153">Encaminhe Olá metadados arquivo toohello caixa equipe de suporte, que configura o logon único para você.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="1d8e8-154">Para a instalação automática de usuários do AD do Azure, no painel esquerdo do hello, selecione **provisionamento**e, em seguida, selecione **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizar o Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="1d8e8-156">Como convidados Dropbox, convidados caixa devem resgatar seu convite de saudação caixa aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1d8e8-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d8e8-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d8e8-157">Next steps</span></span>

<span data-ttu-id="1d8e8-158">Consulte Olá artigos colaboração B2B do Azure AD a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d8e8-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1d8e8-159">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="1d8e8-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1d8e8-160">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1d8e8-161">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1d8e8-162">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1d8e8-163">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1d8e8-164">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d8e8-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1d8e8-165">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1d8e8-166">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1d8e8-167">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="1d8e8-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="1d8e8-168">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="1d8e8-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
