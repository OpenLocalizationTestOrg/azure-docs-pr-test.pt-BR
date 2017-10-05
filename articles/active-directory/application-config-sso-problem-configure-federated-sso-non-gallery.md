---
title: "Problema ao configurar o logon único federado para um aplicativo inexistente na galeria| Microsoft Docs"
description: "Aborda alguns dos problemas comuns que você pode encontrar ao configurar o logon único federado para seu aplicativo SAML personalizado que não está listado na Galeria do Aplicativo Azure AD"
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="04133-103">Problema ao configurar o logon único federado para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="04133-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="04133-104">Se você encontrar um problema ao configurar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04133-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="04133-105">Verifique se seguiu todas as etapas do artigo [Configurando logon único para aplicativos que não estão na galeria de aplicativo do Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="04133-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="04133-106">Não é possível adicionar outra instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="04133-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="04133-107">Para adicionar uma segunda instância de um aplicativo você precisará:</span><span class="sxs-lookup"><span data-stu-id="04133-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="04133-108">Configurar um identificador exclusivo para a segunda instância.</span><span class="sxs-lookup"><span data-stu-id="04133-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="04133-109">Não será possível configurar o mesmo identificador usado para a primeira instância.</span><span class="sxs-lookup"><span data-stu-id="04133-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="04133-110">Configurar um certificado diferente daquele usado para a primeira instância.</span><span class="sxs-lookup"><span data-stu-id="04133-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="04133-111">Se o aplicativo não oferecer suporte a qualquer uma das opções acima.</span><span class="sxs-lookup"><span data-stu-id="04133-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="04133-112">Então, não será possível configurar uma segunda instância.</span><span class="sxs-lookup"><span data-stu-id="04133-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="04133-113">Onde é possível configurar o formato EntityID (Identificador de Usuário)</span><span class="sxs-lookup"><span data-stu-id="04133-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="04133-114">Não será possível selecionar o formato EntityID (Identificador de Usuário) que o Azure AD envia para o aplicativo na resposta após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="04133-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="04133-115">O Azure AD seleciona o formato para o atributo NameID (Identificador de Usuário) com base no valor selecionado ou no formato solicitado pelo aplicativo no AuthRequest do SAML.</span><span class="sxs-lookup"><span data-stu-id="04133-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="04133-116">Para obter mais informações, consulte o artigo [Protocolo SAML de Logon Único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="04133-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="04133-117">Onde obter os metadados do aplicativo ou o certificado do Azure AD</span><span class="sxs-lookup"><span data-stu-id="04133-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="04133-118">Para baixar o certificado ou metadados do aplicativo do Azure AD, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="04133-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="04133-119">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="04133-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="04133-120">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="04133-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="04133-121">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04133-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="04133-122">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="04133-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="04133-123">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="04133-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="04133-124">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="04133-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="04133-125">Selecione o aplicativo para o qual você precisa configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="04133-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="04133-126">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04133-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="04133-127">Vá para a seção **Certificado de Autenticação SAML** e, em seguida, clique no valor da coluna **Download**.</span><span class="sxs-lookup"><span data-stu-id="04133-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="04133-128">Dependendo do aplicativo que exigir a configuração de logon único, você verá a opção para baixar o Certificado ou o XML de Metadados.</span><span class="sxs-lookup"><span data-stu-id="04133-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="04133-129">O Azure AD não fornece uma URL para obter os metadados.</span><span class="sxs-lookup"><span data-stu-id="04133-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="04133-130">Os metadados apenas podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="04133-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="04133-131">Não sei como personalizar declarações SAML enviadas para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="04133-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="04133-132">Para saber como personalizar as declarações de atributo SAML enviadas para seu aplicativo, consulte [Mapeamento de declarações no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="04133-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04133-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04133-133">Next steps</span></span>
[<span data-ttu-id="04133-134">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04133-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
