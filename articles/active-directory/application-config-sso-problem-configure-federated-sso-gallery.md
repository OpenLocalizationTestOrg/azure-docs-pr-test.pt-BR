---
title: "Problema ao configurar o logon único federado para um aplicativo na Galeria do Azure AD | Microsoft Docs"
description: "Aborda alguns dos problemas comuns que você pode encontrar ao configurar o logon único federado usando o SAML para aplicativos que estão listados na Galeria do Aplicativo Azure AD"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="043b0-103">Problema ao configurar o logon único federado para um aplicativo na Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="043b0-104">Se você encontrar um problema ao configurar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="043b0-105">Verifique se seguiu todas as etapas no tutorial para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="043b0-106">Nas configurações de aplicativo há uma documentação embutida sobre como configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="043b0-107">Além disso, é possível acessar a [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo detalhada.</span><span class="sxs-lookup"><span data-stu-id="043b0-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="043b0-108">Não é possível adicionar outra instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="043b0-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="043b0-109">Para adicionar uma segunda instância de um aplicativo você precisará:</span><span class="sxs-lookup"><span data-stu-id="043b0-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="043b0-110">Configurar um identificador exclusivo para a segunda instância.</span><span class="sxs-lookup"><span data-stu-id="043b0-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="043b0-111">Não será possível configurar o mesmo identificador usado para a primeira instância.</span><span class="sxs-lookup"><span data-stu-id="043b0-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="043b0-112">Configurar um certificado diferente daquele usado para a primeira instância.</span><span class="sxs-lookup"><span data-stu-id="043b0-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="043b0-113">Se o aplicativo não oferecer suporte a qualquer uma das opções acima.</span><span class="sxs-lookup"><span data-stu-id="043b0-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="043b0-114">Então, não será possível configurar uma segunda instância.</span><span class="sxs-lookup"><span data-stu-id="043b0-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="043b0-115">Não é possível adicionar o Identificador ou a URL de resposta</span><span class="sxs-lookup"><span data-stu-id="043b0-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="043b0-116">Se não conseguir configurar o Identificador ou a URL de Resposta, confirme se os valores do Identificador e da URL de Resposta correspondem aos padrões pré-configurados para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="043b0-117">Para saber os padrões pré-configurado para o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="043b0-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="043b0-118">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="043b0-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="043b0-119">Vá para a etapa 7.</span><span class="sxs-lookup"><span data-stu-id="043b0-119">Go to step 7.</span></span> <span data-ttu-id="043b0-120">Se você já estiver na folha de configuração do aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="043b0-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="043b0-121">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="043b0-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="043b0-122">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="043b0-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="043b0-123">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="043b0-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="043b0-124">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="043b0-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="043b0-125">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="043b0-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="043b0-126">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="043b0-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="043b0-127">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="043b0-128">Selecione **Logon com base em SAML** da lista suspensa **Modo**.</span><span class="sxs-lookup"><span data-stu-id="043b0-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="043b0-129">Vá para a caixa de texto **Identificador** ou **URL de Resposta** na **Seção Domínio e URLs.**</span><span class="sxs-lookup"><span data-stu-id="043b0-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="043b0-130">Há três maneiras de conhecer os padrões com suporte para o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="043b0-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="043b0-131">Na caixa de texto, são visíveis os padrões com suporte, como um espaço reservado *Examplo:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="043b0-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="043b0-132">Se não houver suporte para o padrão, você verá um ponto de exclamação vermelho quando tentar inserir o valor na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="043b0-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="043b0-133">Se você passar o mouse sobre o ponto de exclamação vermelho, verá os padrões com suporte.</span><span class="sxs-lookup"><span data-stu-id="043b0-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="043b0-134">No tutorial para o aplicativo, também é possível obter informações sobre os padrões com suporte.</span><span class="sxs-lookup"><span data-stu-id="043b0-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="043b0-135">Na seção **Configura o logon único do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="043b0-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="043b0-136">Vá para a etapa de valores configurados na seção **Domínio e URLs**.</span><span class="sxs-lookup"><span data-stu-id="043b0-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="043b0-137">Se os valores não coincidirem com os padrões pré-configurados no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="043b0-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="043b0-138">Você pode:</span><span class="sxs-lookup"><span data-stu-id="043b0-138">You can:</span></span>

-   <span data-ttu-id="043b0-139">Trabalhar com o fornecedor do aplicativo para obter valores que correspondam ao padrão pré-configurado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="043b0-140">Ou, contatar a equipe do Azure AD em <aadapprequest@microsoft.com> ou deixar um comentário no tutorial para solicitar a atualização dos padrões com suporte para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="043b0-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="043b0-141">Onde é possível configurar o formato EntityID (Identificador de Usuário)</span><span class="sxs-lookup"><span data-stu-id="043b0-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="043b0-142">Não será possível selecionar o formato EntityID (Identificador de Usuário) que o Azure AD envia para o aplicativo na resposta após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="043b0-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="043b0-143">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="043b0-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="043b0-144">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="043b0-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="043b0-145">Não é possível encontrar os metadados do Azure AD para concluir a configuração com o aplicativo</span><span class="sxs-lookup"><span data-stu-id="043b0-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="043b0-146">Para baixar o certificado ou metadados do aplicativo do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="043b0-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="043b0-147">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="043b0-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="043b0-148">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="043b0-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="043b0-149">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="043b0-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="043b0-150">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="043b0-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="043b0-151">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="043b0-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="043b0-152">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="043b0-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="043b0-153">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="043b0-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="043b0-154">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="043b0-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="043b0-155">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="043b0-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="043b0-156">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="043b0-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="043b0-157">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="043b0-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="043b0-158">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="043b0-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="043b0-159">Não sei como personalizar declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="043b0-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="043b0-160">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="043b0-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="043b0-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="043b0-161">Next steps</span></span>
[<span data-ttu-id="043b0-162">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="043b0-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
