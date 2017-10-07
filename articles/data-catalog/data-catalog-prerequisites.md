---
title: "pré-requisitos de catálogo de dados aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os pré-requisitos de saudação que necessário tooget Introdução ao Data Catalog do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="5670e-103">Pré-requisitos de Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="5670e-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="5670e-104">Antes de configurar o catálogo de dados do Azure, você precisa tootake respeito algumas coisas.</span><span class="sxs-lookup"><span data-stu-id="5670e-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="5670e-105">Não se preocupe, esse processo não demora.</span><span class="sxs-lookup"><span data-stu-id="5670e-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="5670e-106">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="5670e-106">Azure subscription</span></span>
<span data-ttu-id="5670e-107">tooset o catálogo de dados, você deve ser o proprietário de saudação ou coproprietário de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5670e-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="5670e-108">Assinaturas do Azure ajudam a organizar os recursos de serviço toocloud de acesso, como o catálogo de dados.</span><span class="sxs-lookup"><span data-stu-id="5670e-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="5670e-109">As assinaturas também ajudam a controlar como o uso de recursos é relatado, cobrado e pago.</span><span class="sxs-lookup"><span data-stu-id="5670e-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="5670e-110">Cada assinatura pode ter uma configuração de cobrança e pagamento separada para que você possa ter assinaturas e planos que variam por departamento, projeto, escritório regional e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="5670e-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="5670e-111">Cada serviço de nuvem pertence tooa assinatura e toohave uma assinatura é necessário antes de configurar o catálogo de dados.</span><span class="sxs-lookup"><span data-stu-id="5670e-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="5670e-112">mais, consulte toolearn [gerenciar contas, assinaturas e funções administrativas](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5670e-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="5670e-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5670e-113">Azure Active Directory</span></span>
<span data-ttu-id="5670e-114">tooset o catálogo de dados, você deve estar conectado com uma conta de usuário do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5670e-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="5670e-115">O AD do Azure fornece uma maneira fácil para sua identidade de toomanage de negócios e acesso, tanto na nuvem hello e local.</span><span class="sxs-lookup"><span data-stu-id="5670e-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="5670e-116">Os usuários podem usar uma único conta do trabalho ou escola para nuvem tooany de logon único e o aplicativo da web local.</span><span class="sxs-lookup"><span data-stu-id="5670e-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="5670e-117">Catálogo de dados usa o AD do Azure tooauthenticate entrar.</span><span class="sxs-lookup"><span data-stu-id="5670e-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="5670e-118">mais, consulte toolearn [o que é o Active Directory do Azure?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5670e-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5670e-119">Usando Olá [portal do Azure](http://portal.azure.com/), você pode entrar com uma conta pessoal da Microsoft ou um Azure Active Directory ou de estudante conta.</span><span class="sxs-lookup"><span data-stu-id="5670e-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="5670e-120">tooset o catálogo de dados usando tanto Olá Olá ou o portal do Azure [portal do catálogo de dados](http://www.azuredatacatalog.com), você deve entrar com uma conta do Active Directory do Azure, não uma conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="5670e-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="5670e-121">Configuração de política do Active Directory</span><span class="sxs-lookup"><span data-stu-id="5670e-121">Active Directory policy configuration</span></span>
<span data-ttu-id="5670e-122">Você pode encontrar uma situação em que você pode entrar no portal do catálogo de dados toohello, mas quando você tenta toosign na ferramenta de registro de fonte de dados toohello, encontrar uma mensagem de erro que impede que você entrar.</span><span class="sxs-lookup"><span data-stu-id="5670e-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="5670e-123">Esse comportamento de problema pode ocorrer somente quando você está na rede da empresa de hello, ou isso pode ocorrer apenas quando você está se conectando fora Olá rede da empresa.</span><span class="sxs-lookup"><span data-stu-id="5670e-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="5670e-124">ferramenta de registro de fonte de dados Olá usa autenticação de formulários toovalidate suas credenciais de usuário no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5670e-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="5670e-125">toohelp que você entrar com êxito, um administrador do Active Directory deve habilitar autenticação de formulários Olá política de autenticação Global.</span><span class="sxs-lookup"><span data-stu-id="5670e-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="5670e-126">Na política de autenticação Global do hello, métodos de autenticação podem ser habilitadas separadamente para intranet e extranet conexões, conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="5670e-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="5670e-127">Erros de entrada podem ocorrer se a autenticação de formulários não está habilitada para rede de saudação do qual você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="5670e-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Política de Autenticação Global do Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="5670e-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5670e-129">Next steps</span></span>
<span data-ttu-id="5670e-130">Para obter mais informações, consulte [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="5670e-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
