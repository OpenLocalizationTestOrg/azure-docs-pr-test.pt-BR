---
title: Problemas ao criar um aplicativo de Application Proxy| Microsoft Docs
description: "Como solucionar problemas de criação de aplicativos de Application Proxy no portal de administração do Azure AD"
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="4caee-103">Problemas ao criar um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="4caee-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="4caee-104">Abaixo estão alguns dos problemas comuns que as pessoas enfrentam ao criar um novo aplicativo de Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="4caee-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="4caee-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="4caee-105">Recommended documents</span></span> 

<span data-ttu-id="4caee-106">Para saber mais sobre como criar um aplicativo de Application Proxy por meio do Portal de administração, consulte [publicar aplicativos usando o Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="4caee-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="4caee-107">Se você estiver seguindo as etapas na documentação e estiver recebendo um erro ao criar o aplicativo, consulte os detalhes do erro para obter informações e sugestões para corrigir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4caee-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="4caee-108">A maioria das mensagens de erro incluem uma correção sugerida.</span><span class="sxs-lookup"><span data-stu-id="4caee-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="4caee-109">Itens específicos a serem verificados</span><span class="sxs-lookup"><span data-stu-id="4caee-109">Specific things to check</span></span>

<span data-ttu-id="4caee-110">Para evitar erros comuns, verifique se:</span><span class="sxs-lookup"><span data-stu-id="4caee-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="4caee-111">Você é um administrador com permissão para criar um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="4caee-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="4caee-112">A URL interna é exclusiva</span><span class="sxs-lookup"><span data-stu-id="4caee-112">The internal URL is unique</span></span>

-   <span data-ttu-id="4caee-113">A URL externa é exclusiva</span><span class="sxs-lookup"><span data-stu-id="4caee-113">The external URL is unique</span></span>

-   <span data-ttu-id="4caee-114">As URLs começam com http ou https e terminam com um "/"</span><span class="sxs-lookup"><span data-stu-id="4caee-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="4caee-115">A URL deve ser um nome de domínio, não um endereço IP</span><span class="sxs-lookup"><span data-stu-id="4caee-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="4caee-116">A mensagem de erro deve ser exibida no canto superior direito ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4caee-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="4caee-117">Você também pode selecionar o ícone de notificação para ver as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="4caee-117">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt de notificação](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="4caee-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4caee-119">Next steps</span></span>
[<span data-ttu-id="4caee-120">Habilitar o Proxy de Aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4caee-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
