---
title: "Pré-requisitos do Catálogo de Dados do Azure | Microsoft Docs"
description: "Saiba mais sobre os pré-requisitos necessário para começar a usar o Catálogo de Dados do Azure."
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
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="f4f82-103">Pré-requisitos de Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="f4f82-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="f4f82-104">Você precisa se encarregar algumas questões antes de configurar o Catálogo de Dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f82-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="f4f82-105">Não se preocupe, esse processo não demora.</span><span class="sxs-lookup"><span data-stu-id="f4f82-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="f4f82-106">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f4f82-106">Azure subscription</span></span>
<span data-ttu-id="f4f82-107">Para configurar o Catálogo de Dados, você deve ser o proprietário ou o coproprietário de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f82-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="f4f82-108">As assinaturas do Azure ajudam a organizar o acesso aos recursos de serviço de nuvem como o Catálogo de Dados.</span><span class="sxs-lookup"><span data-stu-id="f4f82-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="f4f82-109">As assinaturas também ajudam a controlar como o uso de recursos é relatado, cobrado e pago.</span><span class="sxs-lookup"><span data-stu-id="f4f82-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="f4f82-110">Cada assinatura pode ter uma configuração de cobrança e pagamento separada para que você possa ter assinaturas e planos que variam por departamento, projeto, escritório regional e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f4f82-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="f4f82-111">Cada serviço de nuvem pertence a uma assinatura e você precisa ter uma assinatura antes de configurar o Catálogo de Dados.</span><span class="sxs-lookup"><span data-stu-id="f4f82-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="f4f82-112">Para saber mais, confira [Gerenciar contas, assinaturas e funções administrativas](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f4f82-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="f4f82-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4f82-113">Azure Active Directory</span></span>
<span data-ttu-id="f4f82-114">Para configurar o Catálogo de Dados, você deve entrar com uma conta de usuário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f4f82-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="f4f82-115">O Azure Active Directory (Azure AD) fornece uma maneira fácil para a sua empresa gerenciar identidades e acesso, tanto na nuvem quanto local.</span><span class="sxs-lookup"><span data-stu-id="f4f82-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="f4f82-116">Os usuários podem usar uma única conta corporativa ou de estudante para logon único em qualquer aplicativo Web local ou em nuvem.</span><span class="sxs-lookup"><span data-stu-id="f4f82-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="f4f82-117">O Catálogo de Dados usa o Azure AD para autenticar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="f4f82-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="f4f82-118">Para saber mais, confira [O que é o Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4f82-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f4f82-119">Usando o [portal do Azure](http://portal.azure.com/), você pode entrar usando uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4f82-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="f4f82-120">Para configurar o Catálogo de Dados usando o portal do Azure ou o [portal do Catálogo de Dados](http://www.azuredatacatalog.com), você deve entrar com uma conta do Azure Active Directory, não com uma conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="f4f82-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="f4f82-121">Configuração de política do Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4f82-121">Active Directory policy configuration</span></span>
<span data-ttu-id="f4f82-122">Poderá haver uma situação em que você consiga entrar no portal do Catálogo de Dados, mas, ao tentar entrar na ferramenta de registro de fonte de dados, receba uma mensagem de erro impedindo a entrada.</span><span class="sxs-lookup"><span data-stu-id="f4f82-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="f4f82-123">Esse comportamento problemático poderá ocorrer somente quando você estiver na rede da empresa ou poderá ocorrer somente quando você estiver se conectando de fora da rede da empresa.</span><span class="sxs-lookup"><span data-stu-id="f4f82-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="f4f82-124">A ferramenta de registro de fonte de dados usa a Autenticação de Formulários para validar suas credenciais de usuário para o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4f82-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="f4f82-125">Para ajudá-lo a entrar com êxito, um administrador do Active Directory deve habilitar a Autenticação de Formulários na Política de Autenticação Global.</span><span class="sxs-lookup"><span data-stu-id="f4f82-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="f4f82-126">Na Política de Autenticação Global, métodos de autenticação podem ser habilitados separadamente para conexões de intranet e extranet, conforme mostrado na seguinte captura de tela.</span><span class="sxs-lookup"><span data-stu-id="f4f82-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="f4f82-127">Erros de conexão poderão ocorrer se a Autenticação de Formulários não estiver habilitada para a rede da qual você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="f4f82-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Política de Autenticação Global do Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="f4f82-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4f82-129">Next steps</span></span>
<span data-ttu-id="f4f82-130">Para obter mais informações, consulte [Configurando políticas de autenticação](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4f82-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
