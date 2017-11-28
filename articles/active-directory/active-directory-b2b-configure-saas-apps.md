---
title: "Configurar aplicativos SaaS para colaboração B2B no Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="9fb9b-103">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="9fb9b-104">A colaboração B2B do Azure Active Directory (Azure AD) funciona com a maioria dos aplicativos que se integra no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="9fb9b-105">Nesta seção, examinaremos as instruções de como configurar alguns aplicativos SaaS populares para usar com o B2B do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="9fb9b-106">Antes de examinarmos as instruções específicas do aplicativo, aqui estão algumas regras gerais:</span><span class="sxs-lookup"><span data-stu-id="9fb9b-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="9fb9b-107">Para a maioria dos aplicativos, a configuração do usuário precisa acontecer manualmente.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="9fb9b-108">Ou seja, os usuários devem ser criados manualmente no aplicativo também.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="9fb9b-109">Para os aplicativos que oferecem suporte para a configuração automática, como o Dropbox, convites separados são criados a partir dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="9fb9b-110">Os usuários devem aceitar cada convite.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="9fb9b-111">Nos atributos do usuário, para atenuar problemas com o disco de perfil do usuário (UDP) danificado nos usuários convidados, sempre defina o **Identificador do Usuário** para **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="9fb9b-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="9fb9b-112">Dropbox Business</span></span>

<span data-ttu-id="9fb9b-113">Para permitir que os usuários façam logon usando suas contas da organização, você deve configurar manualmente o Dropbox Business para usar o Azure AD como um provedor de identidade SAML (Security Assertion Markup Language).</span><span class="sxs-lookup"><span data-stu-id="9fb9b-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="9fb9b-114">Se o Dropbox Business não foi configurado para fazer isso, não poderá solicitar ou, caso contrário, permitirá que os usuários façam logon usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="9fb9b-115">Para adicionar o aplicativo Dropbox Business no Azure AD, selecione **Aplicativos da empresa** no painel esquerdo, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Botão "Adicionar" na página Aplicativos da empresa](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="9fb9b-117">Na janela **Adicionar um aplicativo**, digite **dropbox** na caixa de pesquisa, em seguida, selecione **Dropbox for Business** na lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Procurar "dropbox" na página Adicionar um aplicativo](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="9fb9b-119">Na página **Logon único**, selecione **Logon único** no painel esquerdo, em seguida, digite **user.mail** na caixa **Identificador do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="9fb9b-120">(É definido como UPN por padrão.)</span><span class="sxs-lookup"><span data-stu-id="9fb9b-120">(It's set as UPN by default.)</span></span>

  ![Configurar o logon único para o aplicativo](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="9fb9b-122">Para baixar o certificado a usar para a configuração do Dropbox, selecione **Configurar DropBox**, em seguida, selecione a **URL do Serviço de Logon Único da SAML** na lista.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Baixar o certificado para a configuração do Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="9fb9b-124">Entre no Dropbox com a URL de logon na página **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Página de entrada do Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="9fb9b-126">No menu, selecione **Console Admin**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-126">On the menu, select **Admin Console**.</span></span>

  ![Link "Console Admin" no menu Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="9fb9b-128">Na caixa de diálogo **Autenticação**, selecione **Mais**, carregue o certificado, em seguida, na caixa **URL de Logon**, digite a URL de logon único da SAML.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Link "Mais" na caixa de diálogo Autenticação recolhida](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![A "URL de Logon" na caixa de diálogo Autenticação expandida](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="9fb9b-131">Para configurar a definição automática do usuário no portal do Azure, selecione **Provisionamento** no painel esquerdo, selecione **Automático** na caixa **Modo de Provisionamento**, em seguida, selecione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configurar o provisionamento automático do usuário no portal do Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="9fb9b-133">Depois dos usuários convidados ou membros terem sido configurados no aplicativo Dropbox, eles receberão um convite separado do Dropbox.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="9fb9b-134">Para usar o logon único do Dropbox, os convidados devem aceitar o convite clicando em um link.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="9fb9b-135">Box</span><span class="sxs-lookup"><span data-stu-id="9fb9b-135">Box</span></span>
<span data-ttu-id="9fb9b-136">Você pode permitir que os usuários autentiquem os usuários convidados do Box com sua conta do Azure AD usando a federação com base no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="9fb9b-137">Neste procedimento, é possível carregar os metadados no Box.com.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="9fb9b-138">Adicione o aplicativo Box a partir dos aplicativos da empresa.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="9fb9b-139">Configure o logon único na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="9fb9b-139">Configure single sign-on in the following order:</span></span>

  ![Configurar logon único do Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="9fb9b-141">a.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-141">a.</span></span> <span data-ttu-id="9fb9b-142">Na caixa **URL de Logon**, verifique se a URL de Logon está definida corretamente para o Box no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="9fb9b-143">Essa é a URL do seu locatário Box.com.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="9fb9b-144">Ela deve seguir a convenção de nomenclatura *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="9fb9b-145">O **Identificador** não se aplica a esse aplicativo, mas ainda aparece como um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="9fb9b-146">b.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-146">b.</span></span> <span data-ttu-id="9fb9b-147">Na caixa **Identificador do usuário**, digite **user.mail** (para o SSO das contas de convidado).</span><span class="sxs-lookup"><span data-stu-id="9fb9b-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="9fb9b-148">c.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-148">c.</span></span> <span data-ttu-id="9fb9b-149">Em **Certificado de Assinatura de SAML**, clique em **Criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="9fb9b-150">d.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-150">d.</span></span> <span data-ttu-id="9fb9b-151">Para começar a configurar seu locatário Box.com para usar o Azure AD como um provedor de identidade, baixe o arquivo de metadados e salve-o em sua unidade local.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="9fb9b-152">e.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-152">e.</span></span> <span data-ttu-id="9fb9b-153">Encaminhe o arquivo de metadados para a equipe de suporte do Box, que configura o logon único para você.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="9fb9b-154">Para a configuração automática do usuário do Azure AD, no painel esquerdo, selecione **Provisionamento**, em seguida, selecione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizar o Azure AD a conectar o Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="9fb9b-156">Como os convidados do Dropbox, os convidados do Box também devem resgatar seu convite no aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="9fb9b-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fb9b-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fb9b-157">Next steps</span></span>

<span data-ttu-id="9fb9b-158">Consulte os seguintes artigos na colaboração B2B do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9fb9b-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9fb9b-159">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="9fb9b-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9fb9b-160">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="9fb9b-161">Como adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="9fb9b-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="9fb9b-162">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="9fb9b-163">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="9fb9b-164">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fb9b-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="9fb9b-165">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="9fb9b-166">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="9fb9b-167">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="9fb9b-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="9fb9b-168">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="9fb9b-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
