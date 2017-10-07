---
title: "aaaCharacteristics do Active Directory do Azure locatário intercaction | Microsoft Docs"
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
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="57a6a-103">Entender como interagem vários locatários do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57a6a-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="57a6a-104">No Azure Active Directory (AD do Azure), cada locatário é um recurso completamente independente: Olá de um ponto logicamente independente de outros locatários que você gerencia.</span><span class="sxs-lookup"><span data-stu-id="57a6a-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="57a6a-105">Não há nenhuma relação pai-filho entre locatários.</span><span class="sxs-lookup"><span data-stu-id="57a6a-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="57a6a-106">Essa independência entre locatários inclui independência de recursos, independência administrativa e independência de sincronização.</span><span class="sxs-lookup"><span data-stu-id="57a6a-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="57a6a-107">Independência de recursos</span><span class="sxs-lookup"><span data-stu-id="57a6a-107">Resource independence</span></span>
* <span data-ttu-id="57a6a-108">Se você cria ou excluir um recurso em um locatário, ela não tem efeito sobre qualquer recurso em outro locatário, com exceção de saudação parcial de usuários externos.</span><span class="sxs-lookup"><span data-stu-id="57a6a-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="57a6a-109">Se você usar um de seus nomes de domínio com um locatário, ele não poderá ser usado com nenhum outro locatário.</span><span class="sxs-lookup"><span data-stu-id="57a6a-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="57a6a-110">Independência administrativa</span><span class="sxs-lookup"><span data-stu-id="57a6a-110">Administrative independence</span></span>
<span data-ttu-id="57a6a-111">Se um usuário não administrativo do locatário “Contoso” criar um locatário de teste “Teste”:</span><span class="sxs-lookup"><span data-stu-id="57a6a-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="57a6a-112">Por padrão, o usuário de saudação que cria um locatário é adicionado como um usuário externo nessa novo locatário e função de administrador global Olá atribuído no locatário.</span><span class="sxs-lookup"><span data-stu-id="57a6a-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="57a6a-113">os administradores de saudação do locatário 'Contoso' têm tootenant sem privilégios administrativos diretos 'Test', a menos que um administrador de "Teste" especificamente conceda a eles esses privilégios.</span><span class="sxs-lookup"><span data-stu-id="57a6a-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="57a6a-114">No entanto, os administradores de 'Contoso' podem controlar o acesso tootenant 'Test' se controle de conta de usuário Olá criado 'Test'.</span><span class="sxs-lookup"><span data-stu-id="57a6a-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="57a6a-115">Se você adicionar ou remover uma função de administrador para um usuário em um locatário, o alteração Olá fará não afetam funções de administrador de saudação que Olá usuário tem em outro locatário.</span><span class="sxs-lookup"><span data-stu-id="57a6a-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="57a6a-116">Independência de sincronização</span><span class="sxs-lookup"><span data-stu-id="57a6a-116">Synchronization independence</span></span>
<span data-ttu-id="57a6a-117">Você pode configurar cada Azure independentemente do AD locatário tooget dados sincronizados a partir de uma única instância do:</span><span class="sxs-lookup"><span data-stu-id="57a6a-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="57a6a-118">ferramenta de Connect Olá AD do Azure, toosynchronize dados com uma única floresta do AD.</span><span class="sxs-lookup"><span data-stu-id="57a6a-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="57a6a-119">Olá locatário do Azure Active conector para o Forefront Identity Manager, toosynchronize dados com um ou mais locais florestas e/ou fontes de dados de AD do Azure não.</span><span class="sxs-lookup"><span data-stu-id="57a6a-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="57a6a-120">Adicionar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="57a6a-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="57a6a-121">tooadd um locatário Azure AD em Olá portal do Azure, entrar muito[Olá portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do AD do Azure e, Olá esquerda, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="57a6a-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="57a6a-122">Ao contrário de outros recursos do Azure, os locatários não são recursos filho de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="57a6a-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="57a6a-123">Se sua assinatura do Azure é cancelada ou expirada, você ainda pode acessar os dados de locatário usando o PowerShell do Azure, hello Azure Graph API ou Olá Office 365 Admin Center.</span><span class="sxs-lookup"><span data-stu-id="57a6a-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="57a6a-124">Você também pode associar outra assinatura locatário hello.</span><span class="sxs-lookup"><span data-stu-id="57a6a-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="57a6a-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57a6a-125">Next steps</span></span>
<span data-ttu-id="57a6a-126">Para obter uma visão geral ampla dos problemas de licenciamento e as melhores práticas do Azure AD, consulte [O que é o licenciamento de locatário do Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="57a6a-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
