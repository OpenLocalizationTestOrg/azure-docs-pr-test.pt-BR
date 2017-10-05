---
title: "Como depurar o logon único baseado em SAML nos aplicativos no Azure Active Directory | Microsoft Docs"
description: "Saiba como depurar o logon único baseado em SAML em aplicativos no Active Directory do Azure  "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="58685-103">Como depurar o logon único baseado em SAML em aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="58685-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="58685-104">Ao depurar uma integração de aplicativo baseada em SAML, geralmente é útil usar uma ferramenta como o [Fiddler](http://www.telerik.com/fiddler) para ver a solicitação SAML, a resposta SAML e o token SAML real que é emitido para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58685-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="58685-105">Examinando o token SAML, você pode garantir que todos os atributos necessários, o nome de usuário no assunto SAML e o URI do emissor estejam chegando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="58685-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="58685-106">A resposta do Azure AD que contém o token SAML normalmente é aquela que ocorre depois de um redirecionamento HTTP 302 de https://login.windows.net e é enviada para a **URL de Resposta** do aplicativo configurado.</span><span class="sxs-lookup"><span data-stu-id="58685-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="58685-107">Você pode exibir o token SAML selecionando essa linha e, em seguida, selecionando a guia **Inspetores > WebForms** no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="58685-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="58685-108">Nela, clique com botão direito no valor **SAMLResponse** e selecione **Enviar para TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="58685-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="58685-109">Selecione **De Base64** no menu **Transformar** para decodificar o token e ver seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="58685-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="58685-110">**Observação**: para ver o conteúdo dessa solicitação HTTP, o Fiddler pode solicitar que você configure a descriptografia de tráfego HTTPS, o que você precisará fazer.</span><span class="sxs-lookup"><span data-stu-id="58685-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="58685-111">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="58685-111">Related Articles</span></span>
* [<span data-ttu-id="58685-112">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="58685-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="58685-113">Configurando logon único para aplicativos que não estão na galeria de aplicativo do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="58685-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="58685-114">Como personalizar declarações emitidas no token SAML para aplicativos pré-integrados</span><span class="sxs-lookup"><span data-stu-id="58685-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png