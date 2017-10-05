---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Microsoft Docs"
description: "Saiba como usar a SAP HANA Cloud Platform com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="1e103-103">Tutorial: Integração do Active Directory do Azure com a Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="1e103-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="1e103-104">O objetivo deste tutorial é mostrar a integração do Azure com a Plataforma de Nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="1e103-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1e103-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1e103-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="1e103-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1e103-107">Uma conta da Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="1e103-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="1e103-108">Depois de concluir este tutorial, os usuários do Azure AD que você atribuiu à SAP HANA Cloud Platform poderão fazer logon único no aplicativo usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e103-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="1e103-109">Você precisa implantar seu próprio aplicativo ou assinar um aplicativo em sua conta da Plataforma de Nuvem HANA SAP para testar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1e103-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="1e103-110">Neste tutorial, um aplicativo é implantado na conta.</span><span class="sxs-lookup"><span data-stu-id="1e103-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="1e103-111">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1e103-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="1e103-112">Habilitando a integração de aplicativos para a Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="1e103-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="1e103-113">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="1e103-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="1e103-114">Atribuindo uma função a um usuário</span><span class="sxs-lookup"><span data-stu-id="1e103-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="1e103-115">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="1e103-115">Assigning users</span></span>

<span data-ttu-id="1e103-116">![Cenário](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="1e103-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="1e103-117">Habilitando a integração de aplicativos para a Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="1e103-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="1e103-118">O objetivo desta seção é descrever como habilitar a integração de aplicativos com a Plataforma de Nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="1e103-119">**Para habilitar a integração de aplicativos com a Plataforma de Nuvem HANA SAP, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1e103-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="1e103-120">No Portal de Gerenciamento do Azure, no painel navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e103-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="1e103-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1e103-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1e103-122">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="1e103-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1e103-123">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="1e103-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="1e103-124">![Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="1e103-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1e103-125">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="1e103-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="1e103-126">![Adicionar aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="1e103-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1e103-127">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="1e103-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="1e103-128">![Adicionar um aplicativo da galeria](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="1e103-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1e103-129">Na **caixa de pesquisa**, digite **Plataforma de Nuvem HANA SAP**.</span><span class="sxs-lookup"><span data-stu-id="1e103-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="1e103-130">![Galeria de Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="1e103-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="1e103-131">No painel de resultados, selecione **Plataforma de Nuvem HANA SAP** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e103-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="1e103-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="1e103-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1e103-133">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="1e103-133">Configure single sign-on</span></span>

<span data-ttu-id="1e103-134">O objetivo desta seção é descrever como permitir que os usuários se autentiquem na Plataforma de Nuvem HANA SAP com sua conta do AD do Azure usando federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="1e103-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="1e103-135">Como parte deste procedimento, será necessário carregar um certificado codificado de base 64 no locatário da Plataforma de Nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="1e103-136">Se você não estiver familiarizado com esse procedimento, veja [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1e103-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="1e103-137">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1e103-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1e103-138">No Portal Clássico do Azure, na página de integração de aplicativos do **SAP HANA Cloud Platform**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="1e103-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="1e103-139">![Configurar logon único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1e103-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1e103-140">Na página **Como você deseja que os usuários façam logon na SAP HANA Cloud Platform**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1e103-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="1e103-141">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="1e103-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="1e103-142">Em uma janela diferente do navegador, inicie uma sessão no cockpit do SAP HANA Cloud Platform em https://account.\<host landscape\>.ondemand.com/cockpit (por exemplo: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="1e103-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="1e103-143">Clique na guia **Confiar** .</span><span class="sxs-lookup"><span data-stu-id="1e103-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="1e103-144">![Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confiança")</span><span class="sxs-lookup"><span data-stu-id="1e103-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="1e103-145">Na seção de gerenciamento de confiança, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1e103-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e103-146">![Obter Metadados](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obter Metadados")</span><span class="sxs-lookup"><span data-stu-id="1e103-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="1e103-147">Clique na guia **Provedor de Serviços Local** .</span><span class="sxs-lookup"><span data-stu-id="1e103-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="1e103-148">Para baixar o arquivo de metadados da SAP HANA Cloud Platform, clique em **Obter Metadados**.</span><span class="sxs-lookup"><span data-stu-id="1e103-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="1e103-149">No portal clássico do Azure Active, na página **Configurar URL do Aplicativo**, execute as etapas a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="1e103-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="1e103-150">![Configurar URL do Aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="1e103-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="1e103-151">Na caixa de texto **URL de Logon**, digite a URL usada pelos usuários para entrar no aplicativo **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="1e103-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="1e103-152">Esta é a URL específica da conta de um recurso protegido em seu aplicativo Plataforma de Nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="1e103-153">A URL é baseada no seguinte padrão: *https://\<nomedoaplicativo\>\<nomedaconta\>.\<host landscape\>.ondemand.com/\<caminho\_para\_recurso\_protegido\>* (por exemplo: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="1e103-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="1e103-154">Esta é a URL em seu aplicativo Plataforma de Nuvem HANA SAP que exige que o usuário seja autenticado.</span><span class="sxs-lookup"><span data-stu-id="1e103-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="1e103-155">Abra o arquivo de metadados da SAP HANA Cloud Platform baixado e localize a marca **ns3:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="1e103-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="1e103-156">Copie o valor do atributo **Location** e cole-o na caixa de texto **URL de Resposta da SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="1e103-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="1e103-157">Na página **Configurar logon único na SAP HANA Cloud Platform**, para baixar os metadados, clique em **Baixar metadados** e salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="1e103-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="1e103-158">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="1e103-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="1e103-159">Na ferramenta Cockpit da SAP HANA Cloud Platform, na seção **Provedor de Serviços Local** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1e103-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e103-160">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="1e103-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="1e103-161">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="1e103-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="1e103-162">Para **Tipo de Configuração**, selecione **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="1e103-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="1e103-163">Para **Nome do Provedor Local**, deixe o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="1e103-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="1e103-164">Para gerar um par de chaves **Chave de Assinatura** e um **Certificado de Assinatura**, clique em **Gerar Par de Chaves**.</span><span class="sxs-lookup"><span data-stu-id="1e103-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="1e103-165">Para **Propagação de Entidade**, selecione **Desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="1e103-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="1e103-166">Para **Forçar Autenticação**, selecione **Desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="1e103-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="1e103-167">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1e103-167">Click **Save**.</span></span>

9. <span data-ttu-id="1e103-168">Clique na guia **Provedor de Identidade Confiável** e em **Adicionar Provedor de Identidade Confiável**.</span><span class="sxs-lookup"><span data-stu-id="1e103-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="1e103-169">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="1e103-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1e103-170">Para gerenciar a lista de provedores de identidade confiáveis, será necessário ter escolhido o Tipo de configuração personalizado na seção Provedor de Serviço Local.</span><span class="sxs-lookup"><span data-stu-id="1e103-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="1e103-171">Para o tipo de configuração Padrão, você terá uma confiança implícita e não editável para o Serviço de ID do SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="1e103-172">Para Nenhum, não há configurações de confiança.</span><span class="sxs-lookup"><span data-stu-id="1e103-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="1e103-173">Clique na guia **Geral** e em **Procurar** para carregar o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="1e103-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="1e103-174">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="1e103-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="1e103-175">Depois de carregar o arquivo de metadados, os valores de **URL de Logon Único**, **URL de Logoff Único** e o **Certificado de Assinatura** serão automaticamente populados.</span><span class="sxs-lookup"><span data-stu-id="1e103-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="1e103-176">Clique na guia **Atributos** .</span><span class="sxs-lookup"><span data-stu-id="1e103-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="1e103-177">Na guia **Atributos**, execute a seguinte etapa:</span><span class="sxs-lookup"><span data-stu-id="1e103-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="1e103-178">![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="1e103-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="1e103-179">Clique em **Adicionar Atributo Baseado em Declaração** e adicione os seguintes atributos baseados em declaração:</span><span class="sxs-lookup"><span data-stu-id="1e103-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="1e103-180">Atributo de Asserção</span><span class="sxs-lookup"><span data-stu-id="1e103-180">Assertion Attribute</span></span> | <span data-ttu-id="1e103-181">Atributo de Entidade</span><span class="sxs-lookup"><span data-stu-id="1e103-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="1e103-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="1e103-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="1e103-183">nome</span><span class="sxs-lookup"><span data-stu-id="1e103-183">firstname</span></span> |
    | <span data-ttu-id="1e103-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="1e103-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="1e103-185">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="1e103-185">lastname</span></span> |
    | <span data-ttu-id="1e103-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="1e103-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="1e103-187">email</span><span class="sxs-lookup"><span data-stu-id="1e103-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="1e103-188">A configuração dos Atributos depende de como os aplicativos na HCP são desenvolvidos, isto é, quais atributos eles esperam ter na resposta do SAML e por qual nome (Atributo de Entidade) eles acessam esse atributo no código.</span><span class="sxs-lookup"><span data-stu-id="1e103-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="1e103-189">O **Atributo Padrão** na captura de tela serve apenas para fins de ilustração.</span><span class="sxs-lookup"><span data-stu-id="1e103-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="1e103-190">Ele não é necessário para que o cenário funcione.</span><span class="sxs-lookup"><span data-stu-id="1e103-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="1e103-191">Os nomes e valores do **Atributo de Entidade** mostrados na captura de tela dependerão de como o aplicativo foi desenvolvido.</span><span class="sxs-lookup"><span data-stu-id="1e103-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="1e103-192">É possível que o seu aplicativo precise de mapeamentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="1e103-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="1e103-193">No portal clássico do Azure, na página de diálogo **Configurar logon único na SAP HANA Cloud Platform**, selecione a confirmação de configuração de logon único e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="1e103-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="1e103-194">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="1e103-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="1e103-195">Grupos baseados em asserção</span><span class="sxs-lookup"><span data-stu-id="1e103-195">Assertion-based groups</span></span>
<span data-ttu-id="1e103-196">Como uma etapa opcional, você pode configurar grupos com base na asserção para seu Provedor de Identidade do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e103-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="1e103-197">Usar grupos na Plataforma de Nuvem HANA SAP permite que você atribua dinamicamente um ou mais usuários a uma ou mais funções em seus aplicativos da Plataforma de Nuvem HANA SAP, determinados pelos valores de atributos na asserção SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1e103-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="1e103-198">Por exemplo, se a declaração contém o atributo "*contract=temporary*", talvez seja conveniente que todos os usuários afetados sejam adicionados ao grupo "*TEMPORARY*".</span><span class="sxs-lookup"><span data-stu-id="1e103-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="1e103-199">O grupo “*TEMPORARY*” pode conter uma ou mais funções de um ou mais aplicativos implantados em sua conta da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1e103-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="1e103-200">Use os grupos com base em asserção se desejar atribuir vários usuários simultaneamente a uma ou mais funções de aplicativos em sua conta da Plataforma de Nuvem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1e103-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="1e103-201">Se você quer atribuir apenas um único usuário ou alguns deles a funções específicas, recomendamos atribuí-los diretamente na guia "**Autorizações**" da ferramenta Cockpit da SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1e103-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="1e103-202">Atribuir uma função a um usuário</span><span class="sxs-lookup"><span data-stu-id="1e103-202">Assign a role to a user</span></span>
<span data-ttu-id="1e103-203">Para permitir que os usuários do AD do Azure façam logon na Plataforma de Nuvem HANA SAP, atribua funções a eles na Plataforma de Nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="1e103-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="1e103-204">**Para atribuir uma função a um usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1e103-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="1e103-205">Faça logon em sua ferramenta cockpit da **SAP HANA Cloud Platform** .</span><span class="sxs-lookup"><span data-stu-id="1e103-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="1e103-206">Realize o que é descrito a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e103-206">Perform the following:</span></span>
   
   <span data-ttu-id="1e103-207">![Autorizações](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizações")</span><span class="sxs-lookup"><span data-stu-id="1e103-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="1e103-208">Clique em **Autorização**.</span><span class="sxs-lookup"><span data-stu-id="1e103-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="1e103-209">Clique na guia **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="1e103-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="1e103-210">Na caixa de texto **Usuário** , digite o endereço de email do usuário.</span><span class="sxs-lookup"><span data-stu-id="1e103-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="1e103-211">Clique em **Atribuir** para atribuir uma função ao usuário.</span><span class="sxs-lookup"><span data-stu-id="1e103-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="1e103-212">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1e103-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="1e103-213">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="1e103-213">Assign users</span></span>
<span data-ttu-id="1e103-214">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e103-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1e103-215">**Para atribuir usuários à Plataforma de Nuvem SAP HANA, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1e103-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="1e103-216">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="1e103-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1e103-217">Na página de integração de aplicativos da **SAP HANA Cloud Platform**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="1e103-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1e103-218">![Atribuir Usuários](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="1e103-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="1e103-219">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="1e103-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1e103-220">![Sim](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="1e103-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1e103-221">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1e103-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="1e103-222">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e103-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

