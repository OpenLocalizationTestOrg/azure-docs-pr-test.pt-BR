---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Microsoft Docs"
description: "Saiba como toouse plataforma de nuvem HANA SAP com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="6d407-103">Tutorial: Integração do Active Directory do Azure com a Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="6d407-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="6d407-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="6d407-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d407-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="6d407-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="6d407-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6d407-107">Uma conta da Plataforma de Nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="6d407-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="6d407-108">Após concluir este tutorial, Olá usuários AD do Azure que você atribuiu tooSAP a plataforma de nuvem HANA toosingle capaz de entrada no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d407-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="6d407-109">Você precisa toodeploy seu próprio aplicativo ou assina o aplicativo tooan em sua plataforma de nuvem HANA SAP conta tootest único logon.</span><span class="sxs-lookup"><span data-stu-id="6d407-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="6d407-110">Neste tutorial, um aplicativo é implantado na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d407-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="6d407-111">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d407-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="6d407-112">Habilitando Olá integração de aplicativos para a plataforma de nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="6d407-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="6d407-113">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="6d407-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="6d407-114">Atribuir um usuário de tooa de função</span><span class="sxs-lookup"><span data-stu-id="6d407-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="6d407-115">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="6d407-115">Assigning users</span></span>

<span data-ttu-id="6d407-116">![Cenário](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="6d407-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="6d407-117">Habilitando Olá integração de aplicativos para a plataforma de nuvem HANA SAP</span><span class="sxs-lookup"><span data-stu-id="6d407-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="6d407-118">Olá objetivo desta seção é toooutline como tooenable Olá integração de plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="6d407-119">**integração do aplicativo hello tooenable para a plataforma de nuvem HANA SAP, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d407-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d407-120">No hello Portal de gerenciamento do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d407-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="6d407-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6d407-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6d407-122">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="6d407-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6d407-123">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="6d407-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="6d407-124">![Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="6d407-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6d407-125">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="6d407-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="6d407-126">![Adicionar aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="6d407-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6d407-127">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="6d407-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="6d407-128">![Adicionar um aplicativo da galeria](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="6d407-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6d407-129">Em Olá **caixa de pesquisa**, tipo **plataforma de nuvem HANA SAP**.</span><span class="sxs-lookup"><span data-stu-id="6d407-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="6d407-130">![Galeria de Aplicativos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="6d407-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="6d407-131">No painel de resultados de saudação, selecione **plataforma de nuvem HANA SAP**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6d407-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="6d407-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="6d407-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="6d407-133">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="6d407-133">Configure single sign-on</span></span>

<span data-ttu-id="6d407-134">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSAP plataforma de nuvem HANA com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d407-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="6d407-135">Como parte desse procedimento, será necessário tooupload um locatário de plataforma de nuvem HANA SAP tooyour certificado codificado em base 64.</span><span class="sxs-lookup"><span data-stu-id="6d407-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="6d407-136">Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="6d407-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="6d407-137">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d407-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d407-138">Em Olá portal clássico do Azure, em Olá **plataforma de nuvem HANA SAP** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6d407-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="6d407-139">![Configurar logon único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="6d407-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="6d407-140">Em Olá **como você gostaria usuários toosign em tooSAP plataforma de nuvem HANA** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d407-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="6d407-141">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="6d407-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="6d407-142">Em uma janela de navegador web diferente, faça logon no toohello cockpit da plataforma de nuvem de HANA SAP em https://account. \<host paisagem\>.ondemand.com/cockpit (por exemplo: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="6d407-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="6d407-143">Clique em Olá **confiança** guia.</span><span class="sxs-lookup"><span data-stu-id="6d407-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="6d407-144">![Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confiança")</span><span class="sxs-lookup"><span data-stu-id="6d407-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="6d407-145">Na seção de gerenciamento de confiança, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d407-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6d407-146">![Obter Metadados](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obter Metadados")</span><span class="sxs-lookup"><span data-stu-id="6d407-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="6d407-147">Clique em Olá **provedor de serviço Local** guia.</span><span class="sxs-lookup"><span data-stu-id="6d407-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="6d407-148">Olá toodownload arquivo de metadados da plataforma de nuvem HANA SAP, clique em **obter metadados de**.</span><span class="sxs-lookup"><span data-stu-id="6d407-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="6d407-149">No hello Azure Active portal clássico, em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d407-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="6d407-150">![Configurar URL do Aplicativo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="6d407-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="6d407-151">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada pelo seu toosign usuários em sua **plataforma de nuvem HANA SAP** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d407-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="6d407-152">Isso é Olá URL de conta específica de um recurso protegido em seu aplicativo de plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="6d407-153">Olá URL é baseada no saudação padrão a seguir: *https://\<applicationName\>\<accountName\>.\< host de paisagem\>.ondemand.com/\<caminho\_para\_protegido\_recurso\>*  (por exemplo: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="6d407-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="6d407-154">Esta é a URL Olá em seu aplicativo de plataforma de nuvem HANA SAP que exige Olá tooauthenticate de usuário.</span><span class="sxs-lookup"><span data-stu-id="6d407-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="6d407-155">Abrir o arquivo de metadados de plataforma de nuvem HANA SAP Olá baixado e localize Olá **ns3: assertionconsumerservice** marca.</span><span class="sxs-lookup"><span data-stu-id="6d407-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="6d407-156">Copie o valor Olá Olá **local** de atributo e, em seguida, cole-Olá **URL de resposta de plataforma de nuvem do SAP HANA** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6d407-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="6d407-157">Em Olá **configurar logon único na plataforma de nuvem HANA SAP** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6d407-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="6d407-158">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="6d407-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="6d407-159">Em Olá cockpit da plataforma de nuvem HANA SAP, em Olá **provedor de serviço Local** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d407-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6d407-160">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="6d407-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="6d407-161">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="6d407-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="6d407-162">Para **Tipo de Configuração**, selecione **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="6d407-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="6d407-163">Como **nome do provedor Local**, deixe o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d407-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="6d407-164">toogenerate um **chave de assinatura** e um **certificado de assinatura de** par de chaves, clique em **gerar par de chaves**.</span><span class="sxs-lookup"><span data-stu-id="6d407-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="6d407-165">Para **Propagação de Entidade**, selecione **Desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="6d407-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="6d407-166">Para **Forçar Autenticação**, selecione **Desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="6d407-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="6d407-167">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d407-167">Click **Save**.</span></span>

9. <span data-ttu-id="6d407-168">Clique em Olá **provedor de identidade confiável** guia e, em seguida, clique em **Adicionar provedor de identidade confiável**.</span><span class="sxs-lookup"><span data-stu-id="6d407-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="6d407-169">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="6d407-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6d407-170">lista de saudação toomanage de provedores de identidade confiável, você precisa toohave escolhida Olá tipo de configuração personalizada na Olá seção do provedor de serviço Local.</span><span class="sxs-lookup"><span data-stu-id="6d407-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="6d407-171">Para tipo de configuração padrão, você tem uma toohello confiança implícita e não editável SAP ID de serviço.</span><span class="sxs-lookup"><span data-stu-id="6d407-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="6d407-172">Para Nenhum, não há configurações de confiança.</span><span class="sxs-lookup"><span data-stu-id="6d407-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="6d407-173">Clique em Olá **geral** guia e, em seguida, clique em **procurar** Olá tooupload baixou o arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="6d407-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="6d407-174">![Gerenciamento de Confiança](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gerenciamento de Confiança")</span><span class="sxs-lookup"><span data-stu-id="6d407-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="6d407-175">Depois de carregar o arquivo de metadados de hello, Olá valores para **URL de logon único**, **URL de Logout único** e **certificado de assinatura** são preenchidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6d407-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="6d407-176">Clique em Olá **atributos** guia.</span><span class="sxs-lookup"><span data-stu-id="6d407-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="6d407-177">Em Olá **atributos** guia, execute Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="6d407-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="6d407-178">![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="6d407-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="6d407-179">Clique em **Adicionar atributo**e, em seguida, adicionar Olá seguintes atributos com base em asserção:</span><span class="sxs-lookup"><span data-stu-id="6d407-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="6d407-180">Atributo de Asserção</span><span class="sxs-lookup"><span data-stu-id="6d407-180">Assertion Attribute</span></span> | <span data-ttu-id="6d407-181">Atributo de Entidade</span><span class="sxs-lookup"><span data-stu-id="6d407-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="6d407-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="6d407-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="6d407-183">nome</span><span class="sxs-lookup"><span data-stu-id="6d407-183">firstname</span></span> |
    | <span data-ttu-id="6d407-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="6d407-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="6d407-185">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="6d407-185">lastname</span></span> |
    | <span data-ttu-id="6d407-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="6d407-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="6d407-187">email</span><span class="sxs-lookup"><span data-stu-id="6d407-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="6d407-188">configuração de Olá Olá atributos depende como Olá aplicativos na HCP são desenvolvidos, isto é, quais atributos eles esperam ter na resposta SAML de saudação e por qual nome (atributo de entidade) eles acessam esse atributo no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d407-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="6d407-189">Olá **atributo padrão** em Olá captura de tela é apenas para fins de ilustração.</span><span class="sxs-lookup"><span data-stu-id="6d407-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="6d407-190">Não é necessário o trabalho de cenário de saudação toomake.</span><span class="sxs-lookup"><span data-stu-id="6d407-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="6d407-191">Olá nomes e valores para **atributo de entidade** mostrado no hello captura de tela dependem de como o aplicativo hello é desenvolvido.</span><span class="sxs-lookup"><span data-stu-id="6d407-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="6d407-192">É possível que o seu aplicativo precise de mapeamentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6d407-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="6d407-193">Em Olá portal clássico do Azure, em Olá **configurar logon único na plataforma de nuvem HANA SAP** página de caixa de diálogo, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="6d407-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="6d407-194">![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="6d407-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="6d407-195">Grupos baseados em asserção</span><span class="sxs-lookup"><span data-stu-id="6d407-195">Assertion-based groups</span></span>
<span data-ttu-id="6d407-196">Como uma etapa opcional, você pode configurar grupos com base na asserção para seu Provedor de Identidade do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d407-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="6d407-197">Usar grupos na plataforma de nuvem HANA SAP permite atribuir toodynamically um ou mais tooone de usuários ou mais funções em seus aplicativos de plataforma de nuvem HANA SAP, determinados pelos valores de atributos em Olá SAML 2.0 asserção.</span><span class="sxs-lookup"><span data-stu-id="6d407-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="6d407-198">Por exemplo, se hello asserção contém atributo hello "*contrato = temporário*", convém todos os usuários afetados toobe toohello adicionado grupo"*temporário*".</span><span class="sxs-lookup"><span data-stu-id="6d407-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="6d407-199">grupo Hello "*temporário*" pode conter uma ou mais funções de um ou mais aplicativos implantados em sua conta da plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="6d407-200">Use grupos com base na asserção quando desejar atribuir toosimultaneously muitos tooone de usuários ou mais funções de aplicativos em sua conta da plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="6d407-201">Se você quiser tooassign apenas um único ou pequeno número de usuários toospecific funções, é recomendável atribuí-las diretamente no hello "**autorizações**" guia de cockpit da plataforma de nuvem HANA SAP de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d407-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="6d407-202">Atribuir um usuário de tooa de função</span><span class="sxs-lookup"><span data-stu-id="6d407-202">Assign a role tooa user</span></span>
<span data-ttu-id="6d407-203">Ordem tooenable AD do Azure usuários toolog na plataforma de nuvem HANA SAP, você deve atribuir funções no hello toothem de plataforma de nuvem HANA SAP.</span><span class="sxs-lookup"><span data-stu-id="6d407-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="6d407-204">**tooassign um usuário de tooa de função, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d407-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d407-205">Faça logon no tooyour **plataforma de nuvem HANA SAP** cockpit.</span><span class="sxs-lookup"><span data-stu-id="6d407-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="6d407-206">Execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6d407-206">Perform hello following:</span></span>
   
   <span data-ttu-id="6d407-207">![Autorizações](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizações")</span><span class="sxs-lookup"><span data-stu-id="6d407-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="6d407-208">Clique em **Autorização**.</span><span class="sxs-lookup"><span data-stu-id="6d407-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="6d407-209">Clique em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="6d407-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="6d407-210">Em Olá **usuário** caixa de texto, o endereço de email do usuário do tipo hello.</span><span class="sxs-lookup"><span data-stu-id="6d407-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="6d407-211">Clique em **atribuir** tooassign Olá tooa chave de criptografia.</span><span class="sxs-lookup"><span data-stu-id="6d407-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="6d407-212">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d407-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="6d407-213">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="6d407-213">Assign users</span></span>
<span data-ttu-id="6d407-214">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="6d407-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="6d407-215">**tooassign usuários tooSAP plataforma de nuvem do HANA, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6d407-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d407-216">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="6d407-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6d407-217">Em Olá **plataforma de nuvem HANA SAP** página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="6d407-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6d407-218">![Atribuir Usuários](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="6d407-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="6d407-219">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="6d407-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="6d407-220">![Sim](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="6d407-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6d407-221">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6d407-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="6d407-222">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d407-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

