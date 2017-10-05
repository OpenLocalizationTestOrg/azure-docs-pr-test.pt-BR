---
title: "O Assistente de Segurança do Privileged Identity Management do Azure AD"
description: "Na primeira vez que você usar a extensão Privileged Identity Management do Azure Active Directory, verá um assistente de segurança. Este artigo descreve as etapas para usar o assistente."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="46644-104">Usando o assistente de segurança no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="46644-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="46644-105">Se você for a primeira pessoa a executar o Azure PIM (Privileged Identity Management) para sua organização, verá um assistente.</span><span class="sxs-lookup"><span data-stu-id="46644-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="46644-106">O assistente ajuda você a entender os riscos à segurança de identidades com privilégios e como usar o PIM para reduzir esses riscos.</span><span class="sxs-lookup"><span data-stu-id="46644-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="46644-107">Você não precisará fazer nenhuma alteração nas atribuições de função existentes no assistente, se preferir fazer isso posteriormente.</span><span class="sxs-lookup"><span data-stu-id="46644-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="46644-108">O que esperar</span><span class="sxs-lookup"><span data-stu-id="46644-108">What to expect</span></span>
<span data-ttu-id="46644-109">Antes de sua organização começar a usar o PIM, todas as atribuições de função são permanentes: os usuários sempre estarão sempre nessas funções, mesmo se não precisarem dos privilégios no momento.</span><span class="sxs-lookup"><span data-stu-id="46644-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="46644-110">A primeira etapa do assistente mostra uma lista de funções com privilégios altos e quantos usuários atualmente estão nessas funções.</span><span class="sxs-lookup"><span data-stu-id="46644-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="46644-111">Você poderá analisar uma função específica para saber mais sobre os usuários se um ou mais não forem familiares.</span><span class="sxs-lookup"><span data-stu-id="46644-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="46644-112">A segunda etapa do assistente lhe fornece a oportunidade de alterar as atribuições de função do administrador.</span><span class="sxs-lookup"><span data-stu-id="46644-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="46644-113">É importante que você tenha pelo menos um administrador global e mais de um administrador de função com privilégios com uma conta organizacional (não uma conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="46644-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="46644-114">Se houver apenas um administrador de função com privilégios, a organização não poderá gerenciar o PIM se essa conta for excluída.</span><span class="sxs-lookup"><span data-stu-id="46644-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="46644-115">Além disso, mantenha as atribuições de função permanentes se um usuário tiver uma conta da Microsoft (uma conta que ele usa para entrar nos serviços Microsoft como o Outlook.com e o Skype).</span><span class="sxs-lookup"><span data-stu-id="46644-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="46644-116">Se você planejar exigir o MFA para ativação para essa função, esse usuário será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="46644-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="46644-117">Depois de ter feito alterações, o assistente não aparecerá mais.</span><span class="sxs-lookup"><span data-stu-id="46644-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="46644-118">Na próxima vez que você ou outro administrador de função com privilégios usar o PIM, você verá o painel do PIM.</span><span class="sxs-lookup"><span data-stu-id="46644-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="46644-119">Se você desejar adicionar ou remover usuários das funções ou alterar as atribuições de permanentes para qualificadas, leia mais em [como adicionar ou remover uma função de usuário](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="46644-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="46644-120">Se desejar fornecer aos usuários mais acesso para gerenciar o PIM, leia mais em [como conceder acesso para gerenciar no PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="46644-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46644-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46644-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

