---
title: Problemas para entrar em um aplicativo de desenvolvimento personalizado | Microsoft Docs
description: "Erros comuns que podem impossibilitá-lo de entrar em um aplicativo desenvolvido por você com o Azure AD"
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="d3c0c-103">Problemas para entrar em um aplicativo de desenvolvimento personalizado</span><span class="sxs-lookup"><span data-stu-id="d3c0c-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="d3c0c-104">Há vários erros que podem estar causando a impossibilidade de entrar em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="d3c0c-105">O principal motivo das pessoas se depararem com esse problema está relacionado com aplicativos configurados incorretamente.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="d3c0c-106">Erros relacionados com aplicativos configurados incorretamente</span><span class="sxs-lookup"><span data-stu-id="d3c0c-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="d3c0c-107">Verifique se as configurações do portal correspondem às que você tem no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="d3c0c-108">Especificamente, compare o ID do Aplicativo/Cliente, URLs de Resposta, Chaves/Segredos do Cliente e URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="d3c0c-109">Compare o recurso que você está solicitando acesso no código com as permissões configuradas na guia **Recursos Necessários** para certificar-se de que está solicitando somente os recursos que você configurou.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="d3c0c-110">Consulte [StackOverflow do Azure AD ](http://stackoverflow.com/questions/tagged/azure-active-directory) para quaisquer erros ou problemas semelhantes.</span><span class="sxs-lookup"><span data-stu-id="d3c0c-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3c0c-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3c0c-111">Next steps</span></span>

[<span data-ttu-id="d3c0c-112">Guia do Desenvolvedor do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3c0c-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="d3c0c-113">Consentir e Integrar Aplicativos ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3c0c-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="d3c0c-114">Consentimento e Permissão para Aplicativos Convergidos do Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="d3c0c-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d3c0c-115">StackOverflow do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3c0c-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
