---
title: "Características da interação entre locatários do Azure Active Directory | Microsoft Docs"
description: "Gerenciar os locatários do Azure Active Directory considerando os locatários como recursos totalmente independentes"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="d08b4-103">Entender como interagem vários locatários do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d08b4-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="d08b4-104">No Azure AD (Azure Active Directory), cada locatário é um recurso totalmente independente: um par logicamente independente dos outros locatários gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d08b4-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="d08b4-105">Não há nenhuma relação pai-filho entre locatários.</span><span class="sxs-lookup"><span data-stu-id="d08b4-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="d08b4-106">Essa independência entre locatários inclui independência de recursos, independência administrativa e independência de sincronização.</span><span class="sxs-lookup"><span data-stu-id="d08b4-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="d08b4-107">Independência de recursos</span><span class="sxs-lookup"><span data-stu-id="d08b4-107">Resource independence</span></span>
* <span data-ttu-id="d08b4-108">Se você criar ou excluir um recurso de um locatário, ele não afetará nenhum recurso em outro locatário, com a exceção parcial de usuários externos.</span><span class="sxs-lookup"><span data-stu-id="d08b4-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="d08b4-109">Se você usar um de seus nomes de domínio com um locatário, ele não poderá ser usado com nenhum outro locatário.</span><span class="sxs-lookup"><span data-stu-id="d08b4-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="d08b4-110">Independência administrativa</span><span class="sxs-lookup"><span data-stu-id="d08b4-110">Administrative independence</span></span>
<span data-ttu-id="d08b4-111">Se um usuário não administrativo do locatário “Contoso” criar um locatário de teste “Teste”:</span><span class="sxs-lookup"><span data-stu-id="d08b4-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="d08b4-112">Por padrão, o usuário que cria um locatário é adicionado como um usuário externo nesse novo locatário e é atribuído à função de administrador global nesse locatário.</span><span class="sxs-lookup"><span data-stu-id="d08b4-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="d08b4-113">Os administradores do locatário “Contoso” não têm privilégios administrativos diretos no diretório “Teste”, a menos que um administrador de “Teste” conceda especificamente esses privilégios a eles.</span><span class="sxs-lookup"><span data-stu-id="d08b4-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="d08b4-114">No entanto, os administradores do “Contoso” poderão controlar o acesso ao locatário “Teste” se controlarem a conta de usuário que criou “Teste”.</span><span class="sxs-lookup"><span data-stu-id="d08b4-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="d08b4-115">Se você adicionar ou remover uma função de administrador de um usuário em um locatário, a alteração não afetará as funções de administrador que o usuário tem em outro locatário.</span><span class="sxs-lookup"><span data-stu-id="d08b4-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="d08b4-116">Independência de sincronização</span><span class="sxs-lookup"><span data-stu-id="d08b4-116">Synchronization independence</span></span>
<span data-ttu-id="d08b4-117">Configure cada locatário do Azure AD de maneira independente para sincronizar os dados de uma única instância de:</span><span class="sxs-lookup"><span data-stu-id="d08b4-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="d08b4-118">Ferramenta do Azure AD Connect, para sincronizar dados com uma única floresta do AD.</span><span class="sxs-lookup"><span data-stu-id="d08b4-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="d08b4-119">Conector de locatário do Azure Active Directory para o Forefront Identity Manager, para sincronizar dados com uma ou mais florestas locais e/ou fontes de dados não Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d08b4-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="d08b4-120">Adicionar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d08b4-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="d08b4-121">Para adicionar um locatário do Azure AD no Portal do Azure, entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do Azure AD e, à esquerda, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="d08b4-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="d08b4-122">Ao contrário de outros recursos do Azure, os locatários não são recursos filho de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d08b4-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="d08b4-123">Caso sua assinatura do Azure seja cancelada ou expire, você ainda poderá acessar os dados de locatário usando o Azure PowerShell, a API do Graph do Azure ou o Centro de Administração do Office 365.</span><span class="sxs-lookup"><span data-stu-id="d08b4-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="d08b4-124">Você também pode associar outra assinatura ao locatário.</span><span class="sxs-lookup"><span data-stu-id="d08b4-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="d08b4-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d08b4-125">Next steps</span></span>
<span data-ttu-id="d08b4-126">Para obter uma visão geral ampla dos problemas de licenciamento e as melhores práticas do Azure AD, consulte [O que é o licenciamento de locatário do Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d08b4-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
