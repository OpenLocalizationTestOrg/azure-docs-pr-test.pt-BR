---
title: "aaaProblem Configurando federado SSO para um aplicativo não Galeria | Microsoft Docs"
description: "Resolver alguns problemas comuns hello, que você pode encontrar ao configurar aplicativo SAML personalizado federado único logon tooyour que não esteja listado no hello Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="6fda4-103">Problema ao configurar o logon único federado para um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="6fda4-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="6fda4-104">Se você encontrar um problema ao configurar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6fda4-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="6fda4-105">Verifique se você tiver seguido todas as etapas de saudação artigo Olá [Configurando único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure hello.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="6fda4-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="6fda4-106">Não é possível adicionar outra instância do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="6fda4-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="6fda4-107">tooadd uma segunda instância de um aplicativo, você precisa toobe capaz de:</span><span class="sxs-lookup"><span data-stu-id="6fda4-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="6fda4-108">Configure um identificador exclusivo para a segunda instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fda4-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="6fda4-109">Você não será capaz de tooconfigure Olá mesmo identificador usado para a primeira instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fda4-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="6fda4-110">Configure um certificado diferente que Olá usada para Olá primeira instância.</span><span class="sxs-lookup"><span data-stu-id="6fda4-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="6fda4-111">Se hello aplicativo não oferece suporte a qualquer Olá acima.</span><span class="sxs-lookup"><span data-stu-id="6fda4-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="6fda4-112">Em seguida, não será capaz de tooconfigure uma segunda instância.</span><span class="sxs-lookup"><span data-stu-id="6fda4-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="6fda4-113">Onde definir o formato de ID (identificador de usuário) Olá</span><span class="sxs-lookup"><span data-stu-id="6fda4-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="6fda4-114">Não é o formato de ID (identificador de usuário) do hello tooselect capaz de AD do Azure envia toohello aplicativo em resposta Olá após a autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="6fda4-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="6fda4-115">Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="6fda4-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="6fda4-116">Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção Olá NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="6fda4-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="6fda4-117">Onde obter os metadados do aplicativo hello ou certificado do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6fda4-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="6fda4-118">os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="6fda4-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="6fda4-119">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="6fda4-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6fda4-120">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="6fda4-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6fda4-121">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="6fda4-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6fda4-122">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="6fda4-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6fda4-123">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6fda4-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="6fda4-124">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="6fda4-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6fda4-125">Selecione o aplicativo hello você configurou o logon único.</span><span class="sxs-lookup"><span data-stu-id="6fda4-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="6fda4-126">Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6fda4-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6fda4-127">Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="6fda4-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="6fda4-128">Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="6fda4-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="6fda4-129">AD do Azure não fornece um URL de metadados de saudação de tooget.</span><span class="sxs-lookup"><span data-stu-id="6fda4-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="6fda4-130">Olá metadados somente podem ser recuperados como um arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="6fda4-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="6fda4-131">Não sei como declarações SAML toocustomize enviado tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="6fda4-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="6fda4-132">toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6fda4-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fda4-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fda4-133">Next steps</span></span>
[<span data-ttu-id="6fda4-134">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fda4-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
