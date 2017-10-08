---
title: "aaaHow toodebug baseado no SAML único logon tooapplications no Active Directory do Azure | Microsoft Docs"
description: "Saiba como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="fb699-103">Como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fb699-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="fb699-104">Ao depurar uma integração de aplicativos baseados em SAML, é geralmente útil toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) toosee Olá solicitação SAML, resposta SAML hello e token SAML real Olá emitido toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb699-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="fb699-105">Examinando o token SAML hello, certifique-se de que todos os Olá atributos necessários, Olá nome de usuário no assunto SAML hello e Olá emissor URI são provenientes conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="fb699-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="fb699-106">Olá resposta do AD do Azure que contém o token SAML Olá é normalmente Olá que ocorre após um redirecionamento HTTP 302 de https://login.windows.net e toohello enviado configurado **URL de resposta** do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fb699-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="fb699-107">Você pode exibir o token SAML Olá selecionando essa linha e, em seguida, selecionando Olá **inspetores > WebForms** guia no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="fb699-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="fb699-108">A partir daí, clique com botão direito Olá **SAMLResponse** valor e selecione **enviar tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="fb699-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="fb699-109">Em seguida, selecione **de Base64** de saudação **transformar** menu toodecode Olá token e ver seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="fb699-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="fb699-110">**Observação**: solicitar conteúdo Olá toosee este HTTP, Fiddler pode solicitar que você tooconfigure descriptografia do tráfego HTTPS, o que você precisará toodo.</span><span class="sxs-lookup"><span data-stu-id="fb699-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="fb699-111">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="fb699-111">Related Articles</span></span>
* [<span data-ttu-id="fb699-112">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fb699-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="fb699-113">Configurando um único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="fb699-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="fb699-114">Como tooCustomize as declarações emitidas no hello Token SAML para aplicativos Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="fb699-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png