---
title: "Assistente de segurança aaaThe do Azure AD Privileged Identity Management"
description: "Olá primeira vez que você usar a extensão do Azure Active Directory Privileged Identity Management hello, você verá um Assistente de segurança. Este artigo descreve etapas Olá para usar o Assistente de saudação."
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="79086-104">Usando o Assistente de segurança Olá no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="79086-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="79086-105">Se você estiver Olá de primeira pessoa toorun gerenciamento de identidade com privilégios do Azure (PIM) para sua organização, você verá um assistente.</span><span class="sxs-lookup"><span data-stu-id="79086-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="79086-106">Olá assistente o ajudará a entender os riscos de segurança de saudação de identidades com privilégios e como toouse PIM tooreduce esses riscos.</span><span class="sxs-lookup"><span data-stu-id="79086-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="79086-107">Você não precisa toomake atribuições de função de tooexisting quaisquer alterações no Assistente de saudação, se você preferir toodo-lo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="79086-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="79086-108">Quais tooexpect</span><span class="sxs-lookup"><span data-stu-id="79086-108">What tooexpect</span></span>
<span data-ttu-id="79086-109">Antes do início da sua organização usar o PIM, todas as atribuições de função são permanentes: usuários Olá são sempre essas funções mesmo se eles não precisarem seus privilégios no momento.</span><span class="sxs-lookup"><span data-stu-id="79086-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="79086-110">a primeira etapa saudação do Assistente de saudação mostra uma lista de funções com privilégios altos e quantos usuários estão atualmente nessas funções.</span><span class="sxs-lookup"><span data-stu-id="79086-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="79086-111">Você pode fazer uma busca de tooa determinada função toolearn mais informações sobre os usuários se uma ou mais delas não estiverem familiarizado.</span><span class="sxs-lookup"><span data-stu-id="79086-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="79086-112">a segunda etapa saudação do Assistente de saudação lhe atribuições de função do administrador toochange oportunidade.</span><span class="sxs-lookup"><span data-stu-id="79086-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="79086-113">É importante que você tenha pelo menos um administrador global e mais de um administrador de função com privilégios com uma conta organizacional (não uma conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="79086-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="79086-114">Se houver somente um administrador com privilégios de função, organização de saudação não será capaz de toomanage PIM se essa conta é excluída.</span><span class="sxs-lookup"><span data-stu-id="79086-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="79086-115">Além disso, mantenha as atribuições de função permanente se um usuário tiver uma conta da Microsoft (uma conta que eles usam toosign nos serviços de tooMicrosoft como Skype e Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="79086-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="79086-116">Se você planejar toorequire MFA para ativação para essa função, esse usuário será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="79086-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="79086-117">Depois de ter feito alterações, Assistente de saudação não será exibido.</span><span class="sxs-lookup"><span data-stu-id="79086-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="79086-118">Olá próxima vez que você ou outro administrador com privilégios de função usar Gerenciador, você verá painel PIM hello.</span><span class="sxs-lookup"><span data-stu-id="79086-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="79086-119">Se você seria como tooadd ou remover usuários das funções ou alterar as atribuições de tooeligible permanente, leia mais em [como tooadd ou remover uma função de usuário](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="79086-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="79086-120">Se você quiser toogive mais usuários acessam toomanage PIM, leia mais em [como toogive acessar toomanage no PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="79086-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79086-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79086-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

