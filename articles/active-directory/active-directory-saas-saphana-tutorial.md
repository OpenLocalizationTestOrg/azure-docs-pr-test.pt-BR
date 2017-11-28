---
title: "Tutorial: integração do Azure Active Directory com o SAP HANA | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: a7e73f6ee763d1005ad85935cf2d8f6b24ecf116
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="d4047-103">Tutorial: integração do Azure Active Directory com o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d4047-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="d4047-104">Neste tutorial, você aprenderá a integrar o SAP HANA ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d4047-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4047-105">A integração do SAP HANA ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d4047-105">Integrating SAP HANA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d4047-106">No Azure AD, é possível controlar quem tem acesso ao SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d4047-106">You can control in Azure AD who has access to SAP HANA</span></span>
- <span data-ttu-id="d4047-107">Você pode permitir que os usuários façam logon automaticamente no SAP HANA (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4047-107">You can enable your users to automatically get signed-on to SAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4047-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d4047-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4047-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4047-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4047-110">Prerequisites</span></span>

<span data-ttu-id="d4047-111">Para configurar a integração do Azure AD ao SAP HANA, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d4047-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="d4047-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4047-113">Uma assinatura do SAP HANA habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d4047-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="d4047-114">Uma instância do HANA em execução, seja em qualquer IaaS público, local, em VMs do Azure ou em grandes instâncias SAP no Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="d4047-115">A Interface da Web de Administração do XSA, bem como o HANA Studio instalado na instância do HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-115">The XSA Administration Web Interface as well as HANA Studio installed on the HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="d4047-116">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-116">To test the steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="d4047-117">Teste a integração primeiro no ambiente de desenvolvimento ou de preparo do aplicativo e, em seguida, use o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d4047-117">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="d4047-118">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d4047-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4047-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d4047-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4047-120">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4047-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4047-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d4047-121">Scenario description</span></span>
<span data-ttu-id="d4047-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d4047-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4047-123">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d4047-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4047-124">Adicionar o SAP HANA da galeria</span><span class="sxs-lookup"><span data-stu-id="d4047-124">Adding SAP HANA from the gallery</span></span>
2. <span data-ttu-id="d4047-125">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-the-gallery"></a><span data-ttu-id="d4047-126">Adicionar o SAP HANA da galeria</span><span class="sxs-lookup"><span data-stu-id="d4047-126">Adding SAP HANA from the gallery</span></span>
<span data-ttu-id="d4047-127">Para configurar a integração do SAP HANA ao Azure AD, você precisará adicionar o SAP HANA da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d4047-127">To configure the integration of SAP HANA into Azure AD, you need to add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d4047-128">**Para adicionar o SAP HANA da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d4047-128">**To add SAP HANA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d4047-129">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4047-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="d4047-131">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d4047-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d4047-132">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d4047-132">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="d4047-134">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4047-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="d4047-136">Na caixa de pesquisa, digite **SAP HANA**, selecione **SAP HANA** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4047-136">In the search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button to add the application.</span></span> 

    ![O novo aplicativo](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4047-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4047-139">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP HANA, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d4047-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d4047-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SAP HANA é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4047-140">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="d4047-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-141">In other words, a link relationship between an Azure AD user and the related user in SAP HANA needs to be established.</span></span>

<span data-ttu-id="d4047-142">No SAP HANA, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="d4047-142">In SAP HANA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d4047-143">Para configurar e testar o logon único do Azure AD com o SAP HANA, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d4047-143">To configure and test Azure AD single sign-on with SAP HANA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d4047-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d4047-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d4047-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d4047-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4047-146">**[Criar um usuário de teste do SAP HANA](#creating-a-sap-hana-test-user)** – para ter um equivalente de Brenda Fernandes no SAP HANA vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4047-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4047-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4047-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4047-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d4047-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4047-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4047-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4047-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="d4047-151">**Para configurar o logon único do Azure AD com o SAP HANA, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d4047-151">**To configure Azure AD single sign-on with SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="d4047-152">No Portal do Azure, na página de integração de aplicativos do **SAP HANA**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d4047-152">In the Azure portal, on the **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d4047-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d4047-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="d4047-156">Na seção **Domínio e URLs do SAP HANA**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d4047-156">On the **SAP HANA Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="d4047-158">a.</span><span class="sxs-lookup"><span data-stu-id="d4047-158">a.</span></span> <span data-ttu-id="d4047-159">Na caixa de texto **Identificador**, digite como: `HA100`</span><span class="sxs-lookup"><span data-stu-id="d4047-159">In the **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="d4047-160">b.</span><span class="sxs-lookup"><span data-stu-id="d4047-160">b.</span></span> <span data-ttu-id="d4047-161">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="d4047-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4047-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="d4047-162">These values are not real.</span></span> <span data-ttu-id="d4047-163">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="d4047-163">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d4047-164">Contate a [equipe de suporte ao cliente do SAP HANA](https://cloudplatform.sap.com/contact.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="d4047-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="d4047-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d4047-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="d4047-167">Se o certificado não está ativo, ative-o clicando na caixa de seleção "Tornar o novo certificado ativo" no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4047-167">If certificate is not active then make it active by clicking the “Make new certificate active” checkbox in the Azure AD.</span></span> 

5. <span data-ttu-id="d4047-168">O aplicativo SAP HANA espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="d4047-168">SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d4047-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="d4047-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="d4047-170">Aqui nós mapeamos o **Identificador de Usuário** com a função **ExtractMailPrefix()** função de **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="d4047-170">Here we have mapped the **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="d4047-171">Isso retorna o valor de prefixo de email do usuário que é a ID de usuário único.</span><span class="sxs-lookup"><span data-stu-id="d4047-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="d4047-172">Isto é enviado para o aplicativo SAP HANA em cada resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d4047-172">This is sent to the SAP HANA application in every successful response.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="d4047-174">Na seção **Atributos de Usuário**, na caixa de diálogo **Logon único**:</span><span class="sxs-lookup"><span data-stu-id="d4047-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="d4047-175">a.</span><span class="sxs-lookup"><span data-stu-id="d4047-175">a.</span></span> <span data-ttu-id="d4047-176">Na lista suspensa **Identificador de Usuário**, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="d4047-176">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="d4047-177">b.</span><span class="sxs-lookup"><span data-stu-id="d4047-177">b.</span></span> <span data-ttu-id="d4047-178">Na lista suspensa **Email**, selecione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="d4047-178">In the **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="d4047-179">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d4047-179">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="d4047-181">Para configurar o logon único no lado do **SAP HANA**, faça logon no seu **Console Web XSA do HANA** navegando até o respectivo ponto de extremidade HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d4047-181">To configure single sign-on on **SAP HANA** side, login to your **HANA XSA Web Console**  by browsing to the respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="d4047-182">Na configuração padrão, a URL redireciona a solicitação para uma tela de logon, o que exige as credenciais de um usuário de banco de dados SAP HANA autenticado para concluir o processo de logon.</span><span class="sxs-lookup"><span data-stu-id="d4047-182">In the default configuration, the URL redirects the request to a logon screen, which requires the credentials of an authenticated SAP HANA database user to complete the logon process.</span></span> <span data-ttu-id="d4047-183">O usuário que fizer logon deverá ter os privilégios necessários para executar tarefas de administração de SAML.</span><span class="sxs-lookup"><span data-stu-id="d4047-183">The user who logs on must have the privileges required to perform SAML administration tasks.</span></span>

9. <span data-ttu-id="d4047-184">Na Interface da Web XSA, navegue até **Provedor de identidade SAML** e clique no botão **"+"** na parte inferior da tela para exibir o painel Adicionar Informações de Provedor de Identidade e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d4047-184">In the XSA Web Interface, navigate to **SAML Identity Provider** and from there, click the **“+”** -button on the bottom of the screen to display the Add Identity Provider Info pane and perform the following steps:</span></span>

    ![Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="d4047-186">a.</span><span class="sxs-lookup"><span data-stu-id="d4047-186">a.</span></span> <span data-ttu-id="d4047-187">No painel **Adicionar Informações do Provedor de Identidade**, cole o conteúdo do XML de metadados que você baixou do Portal do Azure na caixa de texto **Metadados**.</span><span class="sxs-lookup"><span data-stu-id="d4047-187">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML, which you have downloaded from Azure portal into the **Metadata** textbox.</span></span>

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="d4047-189">b.</span><span class="sxs-lookup"><span data-stu-id="d4047-189">b.</span></span> <span data-ttu-id="d4047-190">Se o conteúdo do documento XML é válido, o processo de análise extrai as informações necessárias para inserir os campos **Assunto, ID de Entidade e Emissor** na área Dados Gerais da tela e os campos de URL na área Destino da tela, por exemplo, **URL Base e a URL SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="d4047-190">If the contents of the XML document are valid, the parsing process extracts the information required to insert into the **Subject, Entity ID, and Issuer** fields in the General Data screen area, and the URL fields in the Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="d4047-192">c.</span><span class="sxs-lookup"><span data-stu-id="d4047-192">c.</span></span> <span data-ttu-id="d4047-193">Na caixa Nome da área Dados Gerais da tela, insira um nome para o novo provedor de identidade SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="d4047-193">In the Name box of the General Data screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="d4047-194">O nome do IdP de SAML é obrigatório e deve ser exclusivo. Ele aparecerá na lista de IdPs de SAML disponíveis que é exibida, se você selecionar SAML como o método de autenticação para aplicativos XS do SAP HANA a usar, por exemplo, na área de Autenticação da tela da ferramenta de Administração de Artefato XS.</span><span class="sxs-lookup"><span data-stu-id="d4047-194">The name of the SAML IDP is mandatory and must be unique; it appears in the list of available SAML IDPs that is displayed, if you select SAML as the authentication method for SAP HANA XS applications to use, for example, in the Authentication screen area of the XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="d4047-195">Salve os detalhes do novo provedor de identidade SAML.</span><span class="sxs-lookup"><span data-stu-id="d4047-195">Save the details of the new SAML identity provider.</span></span> <span data-ttu-id="d4047-196">Escolha **Salvar** para salvar os detalhes do provedor de identidade SAML e adicione o novo IdP de SAML à lista de IdPs de SAML conhecidos.</span><span class="sxs-lookup"><span data-stu-id="d4047-196">Choose **Save** to save the details of the SAML identity provider and add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![botão salvar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="d4047-198">No HANA Studio, dentro das propriedades do sistema da guia **Configuração**, apenas filtre as configurações por **saml** e ajuste o **assertion_timeout** de **10 s** para **120 s**.</span><span class="sxs-lookup"><span data-stu-id="d4047-198">In HANA Studio within the system properties of the **Configuration** tab, just filter settings by **saml** and adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![configuração assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="d4047-200">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d4047-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d4047-201">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d4047-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d4047-202">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4047-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4047-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4047-204">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d4047-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d4047-206">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d4047-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d4047-207">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4047-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4047-209">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d4047-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4047-211">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4047-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4047-213">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d4047-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4047-215">a.</span><span class="sxs-lookup"><span data-stu-id="d4047-215">a.</span></span> <span data-ttu-id="d4047-216">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d4047-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4047-217">b.</span><span class="sxs-lookup"><span data-stu-id="d4047-217">b.</span></span> <span data-ttu-id="d4047-218">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d4047-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4047-219">c.</span><span class="sxs-lookup"><span data-stu-id="d4047-219">c.</span></span> <span data-ttu-id="d4047-220">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d4047-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d4047-221">d.</span><span class="sxs-lookup"><span data-stu-id="d4047-221">d.</span></span> <span data-ttu-id="d4047-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d4047-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="d4047-223">Criação de um usuário de teste SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d4047-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="d4047-224">Para permitir que os usuários do Azure AD façam logon no SAP HANA, eles devem ser provisionados no SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-224">To enable Azure AD users to log in to SAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="d4047-225">O SAP HANA dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d4047-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d4047-226">Se você precisar criar um usuário manualmente, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d4047-226">If you need to create a user manually, perform the following steps:</span></span>

>[!Note]
><span data-ttu-id="d4047-227">Você pode alterar a autenticação externa usada pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="d4047-227">You can change the external authentication used by the user.</span></span>
<span data-ttu-id="d4047-228">Os usuários externos são autenticados usando um sistema externo, por exemplo, um sistema Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d4047-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="d4047-229">Para obter informações detalhadas sobre identidades externas, contate seu [administrador de domínio](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="d4047-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="d4047-230">Abra o [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como administrador e habilite o usuário do BD para o SSO do SAML.</span><span class="sxs-lookup"><span data-stu-id="d4047-230">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable the DB-User for SAML SSO.</span></span>

    ![criar usuário](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="d4047-232">Marque a caixa de seleção invisível à esquerda do **SAML** e siga o link Configurar.</span><span class="sxs-lookup"><span data-stu-id="d4047-232">Tick the invisible checkbox to the left of **SAML** and follow the Configure link.</span></span>

3. <span data-ttu-id="d4047-233">Clique em **Adicionar** para adicionar o IdP de SAML e clique em **OK** selecionando o IdP de SAML apropriado.</span><span class="sxs-lookup"><span data-stu-id="d4047-233">Click **Add** to add the SAML IDP and click **OK** selecting the appropriate SAML IDP.</span></span>

4. <span data-ttu-id="d4047-234">Adicione a **Identidade Externa** (por ex.,</span><span class="sxs-lookup"><span data-stu-id="d4047-234">Add the **External Identity** (ex.</span></span> <span data-ttu-id="d4047-235">BrendaFernandes aqui) ou escolha **"Qualquer"** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4047-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="d4047-236">Se a caixa de seleção "QUALQUER" não estiver marcada, o nome de usuário no HANA deverá corresponder exatamente ao nome do usuário no nome UPN antes do sufixo de domínio (ou seja, BrittaSimon@contoso.com se tornaria BrendaFernandes no HANA).</span><span class="sxs-lookup"><span data-stu-id="d4047-236">If "ANY" check-box is not checked, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="d4047-237">Para fins de teste, atribua todas as funções **"XS"** ao usuário.</span><span class="sxs-lookup"><span data-stu-id="d4047-237">For testing purposes, assign all **"XS"** roles to the user.</span></span>

    ![atribuição de funções](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="d4047-239">Você deve conceder apenas as permissões apropriadas para seus casos de uso.</span><span class="sxs-lookup"><span data-stu-id="d4047-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="d4047-240">Salve o usuário.</span><span class="sxs-lookup"><span data-stu-id="d4047-240">Save the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d4047-241">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d4047-242">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="d4047-244">**Para atribuir Brenda Fernandes ao SAP HANA, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d4047-244">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="d4047-245">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d4047-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d4047-247">Na lista de aplicativos, selecione **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="d4047-247">In the applications list, select **SAP HANA**.</span></span>

    ![Atribuir usuário](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="d4047-249">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d4047-249">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="d4047-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4047-251">Click **Add** button.</span></span> <span data-ttu-id="d4047-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4047-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="d4047-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d4047-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d4047-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4047-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4047-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4047-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4047-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d4047-257">Testing single sign-on</span></span>

<span data-ttu-id="d4047-258">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d4047-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d4047-259">Ao clicar no bloco do SAP HANA no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="d4047-259">When you click the SAP HANA tile in the Access Panel, you should get automatically signed-on to your SAP HANA application.</span></span>
<span data-ttu-id="d4047-260">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d4047-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4047-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d4047-261">Additional resources</span></span>

* [<span data-ttu-id="d4047-262">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d4047-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4047-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4047-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

