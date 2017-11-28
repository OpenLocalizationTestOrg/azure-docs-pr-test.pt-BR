---
title: "aaaUnlicensed relatório de uso | Microsoft Docs"
description: "Olá relatório de uso não licenciado paga de ajuda a que identificar os usuários não licenciados que estão usando recursos do AD do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="fd417-103">Relatório de uso não licenciado</span><span class="sxs-lookup"><span data-stu-id="fd417-103">Unlicensed usage report</span></span>
<span data-ttu-id="fd417-104">Olá relatório de uso não licenciado paga de ajuda a que identificar os usuários não licenciados que estão usando recursos do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd417-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="fd417-105">Isso permite toomake melhor uso de licenças que você comprou e tooidentify você saber quando você pode precisar de mais licenças.</span><span class="sxs-lookup"><span data-stu-id="fd417-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="fd417-106">relatório de saudação mostra o uso ativo de Olá recursos pago no hello últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="fd417-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="fd417-107">Estrutura de relatório</span><span class="sxs-lookup"><span data-stu-id="fd417-107">Report structure</span></span>
| <span data-ttu-id="fd417-108">Nome da coluna</span><span class="sxs-lookup"><span data-stu-id="fd417-108">Column name</span></span> | <span data-ttu-id="fd417-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="fd417-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fd417-110">Usuário Não Licenciado</span><span class="sxs-lookup"><span data-stu-id="fd417-110">Unlicensed User</span></span> |<span data-ttu-id="fd417-111">Nome de usuário de saudação</span><span class="sxs-lookup"><span data-stu-id="fd417-111">Name of hello user</span></span> |
| <span data-ttu-id="fd417-112">Recurso</span><span class="sxs-lookup"><span data-stu-id="fd417-112">Feature</span></span> |<span data-ttu-id="fd417-113">nome do recurso Hello.</span><span class="sxs-lookup"><span data-stu-id="fd417-113">hello feature name.</span></span> <span data-ttu-id="fd417-114">Por exemplo: acesso condicional</span><span class="sxs-lookup"><span data-stu-id="fd417-114">For example: conditional access</span></span> |
| <span data-ttu-id="fd417-115">Aplicativo acessado</span><span class="sxs-lookup"><span data-stu-id="fd417-115">Application Accessed</span></span> |<span data-ttu-id="fd417-116">nome de saudação do aplicativo de saudação que está sendo acessado com recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd417-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="fd417-117">Por exemplo: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fd417-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="fd417-118">Se uma conta de usuário foi excluída Olá 'Não licenciado User' coluna será preenchida com uma ID, como 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="fd417-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="fd417-119">Recurso de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="fd417-119">Conditional access feature</span></span>
<span data-ttu-id="fd417-120">Os usuários não licenciados serão sinalizados quando acessarem um serviço com a política de acesso condicional aplicada se não tiverem uma licença do Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="fd417-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="fd417-121">Isso se aplica a tooMFA / políticas de local, bem como dispositivo políticas que usar o Intune.</span><span class="sxs-lookup"><span data-stu-id="fd417-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="fd417-122">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fd417-122">See also</span></span>
* [<span data-ttu-id="fd417-123">Usar o acesso condicional com o Office 365 e com outros aplicativos conectados ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd417-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="fd417-124">Introdução ao acesso condicional tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="fd417-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

