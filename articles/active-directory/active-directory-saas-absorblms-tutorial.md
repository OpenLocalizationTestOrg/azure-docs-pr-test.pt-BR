---
title: "Tutorial: Integração do Azure Active Directory ao Absorb LMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Absorb LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="0a569-103">Tutorial: Integração do Azure Active Directory ao Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="0a569-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="0a569-104">Neste tutorial, você aprenderá a integrar o Absorb LMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0a569-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a569-105">A integração do Absorb LMS ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0a569-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a569-106">É possível controlar no Azure AD quem tem acesso ao Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="0a569-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="0a569-107">Você pode permitir que seus usuários entrem automaticamente no Absorb LMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a569-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a569-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a569-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a569-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="0a569-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0a569-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a569-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a569-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0a569-111">Prerequisites</span></span>

<span data-ttu-id="0a569-112">Para configurar a integração do Azure AD ao Absorb LMS, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0a569-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="0a569-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a569-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0a569-114">Uma assinatura do Absorb LMS com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="0a569-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a569-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0a569-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a569-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0a569-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a569-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0a569-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a569-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a569-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a569-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0a569-119">Scenario description</span></span>
<span data-ttu-id="0a569-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0a569-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a569-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0a569-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a569-122">Adicionar o Absorb LMS da Galeria</span><span class="sxs-lookup"><span data-stu-id="0a569-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="0a569-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a569-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="0a569-124">Adicionar o Absorb LMS da Galeria</span><span class="sxs-lookup"><span data-stu-id="0a569-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="0a569-125">Para configurar a integração do Absorb LMS com o Azure AD, você precisa adicionar o Absorb LMS da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0a569-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a569-126">**Para adicionar o Absorb LMS da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0a569-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a569-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a569-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="0a569-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0a569-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a569-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0a569-130">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="0a569-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0a569-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="0a569-134">Na caixa de pesquisa, digite **Absorb LMS**, selecione **Absorb LMS** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0a569-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![Absorb LMS na lista de resultados](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0a569-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a569-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0a569-137">Nesta seção, você configurará e testará o logon único do Azure AD com o Absorb LMS, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="0a569-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a569-138">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Absorb LMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a569-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="0a569-139">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0a569-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="0a569-140">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0a569-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="0a569-141">Para configurar e testar o logon único do Azure AD com o Absorb LMS, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0a569-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a569-142">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0a569-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a569-143">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a569-144">**[Criar um usuário de teste do Absorb LMS](#create-an-absorb-lms-test-user)** – para ter um equivalente de Brenda Fernandes no Absorb LMS que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a569-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a569-145">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a569-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a569-146">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0a569-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0a569-147">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a569-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0a569-148">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0a569-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="0a569-149">**Para configurar o logon único do Azure AD com o Absorb LMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0a569-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a569-150">No Portal do Azure, na página de integração de aplicativos do **Absorb LMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0a569-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="0a569-152">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0a569-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="0a569-154">Na seção **Domínio e URLs do Absorb LMS**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0a569-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="0a569-156">a.</span><span class="sxs-lookup"><span data-stu-id="0a569-156">a.</span></span> <span data-ttu-id="0a569-157">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="0a569-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="0a569-158">b.</span><span class="sxs-lookup"><span data-stu-id="0a569-158">b.</span></span> <span data-ttu-id="0a569-159">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="0a569-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0a569-160">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="0a569-160">These values are not the real.</span></span> <span data-ttu-id="0a569-161">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="0a569-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0a569-162">Contate a [equipe de suporte do cliente Absorb LMS](https://www.absorblms.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="0a569-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="0a569-163">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0a569-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="0a569-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0a569-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0a569-167">Na seção **Configuração do Absorb LMS**, clique em **Configurar Absorb LMS** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="0a569-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a569-168">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0a569-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="0a569-170">Em outra janela do navegador da Web, faça logon em seu site de empresa Absorb LMS como um administrador.</span><span class="sxs-lookup"><span data-stu-id="0a569-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="0a569-171">Clique no **Ícone de Conta** na interface de administrador.</span><span class="sxs-lookup"><span data-stu-id="0a569-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="0a569-173">Clique em **Configurações do Portal**.</span><span class="sxs-lookup"><span data-stu-id="0a569-173">Click **Portal Settings**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="0a569-175">Clique na guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="0a569-175">Click the **Users** tab.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="0a569-177">Para acessar os campos de configuração de logon único, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0a569-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="0a569-179">a.</span><span class="sxs-lookup"><span data-stu-id="0a569-179">a.</span></span> <span data-ttu-id="0a569-180">Selecione o **Modo** adequado.</span><span class="sxs-lookup"><span data-stu-id="0a569-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="0a569-181">b.</span><span class="sxs-lookup"><span data-stu-id="0a569-181">b.</span></span> <span data-ttu-id="0a569-182">Abra o certificado que você baixou do Portal do Azure no bloco de notas, remova a marcação **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** e, em seguida, cole o conteúdo restante na caixa de texto **Chave**.</span><span class="sxs-lookup"><span data-stu-id="0a569-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="0a569-183">c.</span><span class="sxs-lookup"><span data-stu-id="0a569-183">c.</span></span> <span data-ttu-id="0a569-184">Na **Propriedade ID**, selecione o atributo apropriado que você configurou como o identificador de usuário no Azure AD (por exemplo, se o userprinciplename fosse selecionado no Azure AD, o nome de usuário seria selecionado aqui.)</span><span class="sxs-lookup"><span data-stu-id="0a569-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="0a569-185">d.</span><span class="sxs-lookup"><span data-stu-id="0a569-185">d.</span></span> <span data-ttu-id="0a569-186">No **URL de logon**, cole o valor de **"URL de Logon Único do Serviço SAML"** copiado da janela **Configurar logon** do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a569-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="0a569-187">e.</span><span class="sxs-lookup"><span data-stu-id="0a569-187">e.</span></span> <span data-ttu-id="0a569-188">No **URL de logout**, cole o valor de **"URL de Saída"** copiado da janela **Configurar logon** do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a569-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="0a569-189">Habilitar **"Permitir apenas logon SSO"**.</span><span class="sxs-lookup"><span data-stu-id="0a569-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="0a569-191">Clique em **"Salvar".**</span><span class="sxs-lookup"><span data-stu-id="0a569-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="0a569-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0a569-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a569-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0a569-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a569-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a569-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0a569-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a569-195">Create an Azure AD test user</span></span>

<span data-ttu-id="0a569-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="0a569-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0a569-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a569-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a569-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a569-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0a569-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a569-203">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a569-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a569-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0a569-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a569-207">a.</span><span class="sxs-lookup"><span data-stu-id="0a569-207">a.</span></span> <span data-ttu-id="0a569-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0a569-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a569-209">b.</span><span class="sxs-lookup"><span data-stu-id="0a569-209">b.</span></span> <span data-ttu-id="0a569-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a569-211">c.</span><span class="sxs-lookup"><span data-stu-id="0a569-211">c.</span></span> <span data-ttu-id="0a569-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0a569-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a569-213">d.</span><span class="sxs-lookup"><span data-stu-id="0a569-213">d.</span></span> <span data-ttu-id="0a569-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0a569-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="0a569-215">Criar um usuário de teste do Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="0a569-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="0a569-216">Para permitir que os usuários do Azure AD façam logon no Absorb LMS, eles devem ser provisionados no Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0a569-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="0a569-217">Para o Absorb LMS, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="0a569-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="0a569-218">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0a569-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0a569-219">Faça logon em seu site de empresa do Absorb LMS como administrador.</span><span class="sxs-lookup"><span data-stu-id="0a569-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="0a569-220">Clique na guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="0a569-220">Click **Users** tab.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="0a569-222">Clique em **Usuários** sob a guia **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="0a569-222">Click **Users** under the **Users** tab.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="0a569-224">Selecione **Usuário** da lista suspensa **Adicionar Novo**.</span><span class="sxs-lookup"><span data-stu-id="0a569-224">Select **User** from **Add New** drop-down.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="0a569-226">Na página **Adicionar Usuário**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0a569-226">On the **Add User** page, perform the following steps:</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="0a569-228">a.</span><span class="sxs-lookup"><span data-stu-id="0a569-228">a.</span></span> <span data-ttu-id="0a569-229">Na caixa de texto **Nome**, digite o nome do usuário como Brenda.</span><span class="sxs-lookup"><span data-stu-id="0a569-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="0a569-230">b.</span><span class="sxs-lookup"><span data-stu-id="0a569-230">b.</span></span> <span data-ttu-id="0a569-231">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="0a569-232">c.</span><span class="sxs-lookup"><span data-stu-id="0a569-232">c.</span></span> <span data-ttu-id="0a569-233">Na caixa de texto **Nome de usuário**, digite o nome de usuário como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="0a569-234">d.</span><span class="sxs-lookup"><span data-stu-id="0a569-234">d.</span></span> <span data-ttu-id="0a569-235">Na caixa de texto **Senha**, digite a senha de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0a569-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="0a569-236">e.</span><span class="sxs-lookup"><span data-stu-id="0a569-236">e.</span></span> <span data-ttu-id="0a569-237">Na caixa de texto **Confirmar Senha**, digite a mesma senha.</span><span class="sxs-lookup"><span data-stu-id="0a569-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="0a569-238">f.</span><span class="sxs-lookup"><span data-stu-id="0a569-238">f.</span></span> <span data-ttu-id="0a569-239">Torne-a **ATIVA**.</span><span class="sxs-lookup"><span data-stu-id="0a569-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="0a569-240">Clique em **"Salvar".**</span><span class="sxs-lookup"><span data-stu-id="0a569-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0a569-241">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a569-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="0a569-242">Nesta seção, você concederá acesso ao Absorb LMS a Brenda Fernandes para habilitá-la a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a569-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="0a569-244">**Para atribuir Brenda Fernandes ao Absorb LMS, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0a569-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a569-245">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0a569-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0a569-247">Na lista de aplicativos, selecione **Absorb LMS**.</span><span class="sxs-lookup"><span data-stu-id="0a569-247">In the applications list, select **Absorb LMS**.</span></span>

    ![O link do Absorb LMS na lista Aplicativos](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="0a569-249">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a569-249">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="0a569-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0a569-251">Click **Add** button.</span></span> <span data-ttu-id="0a569-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a569-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="0a569-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0a569-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a569-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a569-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a569-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a569-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0a569-257">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="0a569-257">Test single sign-on</span></span>

<span data-ttu-id="0a569-258">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0a569-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a569-259">Clique no bloco Absorb LMS no Painel de Acesso, você será conectado automaticamente ao seu aplicativo Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0a569-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="0a569-260">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0a569-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a569-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0a569-261">Additional resources</span></span>

* [<span data-ttu-id="0a569-262">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0a569-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a569-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a569-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

