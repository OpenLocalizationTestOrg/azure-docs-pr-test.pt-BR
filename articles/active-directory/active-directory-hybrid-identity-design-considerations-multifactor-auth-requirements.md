---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de autenticação multifator"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="7579d-104">Determinar os requisitos de autenticação multifator para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="7579d-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="7579d-105">Em um mundo de mobilidade com usuários que acessam dados e aplicativos em nuvem hello e de qualquer dispositivo, proteger essas informações se torna muito importante.</span><span class="sxs-lookup"><span data-stu-id="7579d-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="7579d-106">Todos os dias há um novo título sobre violação de segurança.</span><span class="sxs-lookup"><span data-stu-id="7579d-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="7579d-107">Embora, não há nenhuma garantia contra falhas desse tipo, a autenticação multifator, fornece uma camada adicional de segurança toohelp evitar essas violações.</span><span class="sxs-lookup"><span data-stu-id="7579d-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="7579d-108">Iniciar avaliação de requisitos de organizações Olá para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="7579d-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="7579d-109">Ou seja, o que é Olá organização tentar toosecure.</span><span class="sxs-lookup"><span data-stu-id="7579d-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="7579d-110">Essa avaliação é requisitos técnicos do hello toodefine importantes para configurar e habilitar os usuários de organizações Olá para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="7579d-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="7579d-111">Se você não estiver familiarizado com o MFA e o que ele faz, ela é altamente recomendável que você leia o artigo Olá [o que é o Azure multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue anterior ler esta seção.</span><span class="sxs-lookup"><span data-stu-id="7579d-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="7579d-112">Verifique a seguir Olá tooanswer-se de que:</span><span class="sxs-lookup"><span data-stu-id="7579d-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="7579d-113">Sua empresa está tentando toosecure aplicativos da Microsoft?</span><span class="sxs-lookup"><span data-stu-id="7579d-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="7579d-114">Como esses aplicativos são publicados?</span><span class="sxs-lookup"><span data-stu-id="7579d-114">How these apps are published?</span></span>
* <span data-ttu-id="7579d-115">Sua empresa oferece acesso remoto tooallow funcionários tooaccess local aplicativos?</span><span class="sxs-lookup"><span data-stu-id="7579d-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="7579d-116">Em caso afirmativo, que tipo de acesso remoto? Você também precisa tooevaluate onde os usuários de saudação que acessam esses aplicativos serão localizados.</span><span class="sxs-lookup"><span data-stu-id="7579d-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="7579d-117">Essa avaliação é outra estratégia de autenticação multifator adequada etapa importante toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="7579d-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="7579d-118">Certifique-se de saudação tooanswer perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7579d-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="7579d-119">Onde estão localizados os usuários Olá vai toobe?</span><span class="sxs-lookup"><span data-stu-id="7579d-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="7579d-120">Podem ser localizados em qualquer lugar?</span><span class="sxs-lookup"><span data-stu-id="7579d-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="7579d-121">Sua empresa deseja tooestablish restrições de acordo com o local do usuário toohello?</span><span class="sxs-lookup"><span data-stu-id="7579d-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="7579d-122">Depois de compreender esses requisitos, é importante tooalso avaliar Olá requisitos de usuário para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="7579d-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="7579d-123">Essa avaliação é importante porque ele definirá requisitos Olá para implementar a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="7579d-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="7579d-124">Certifique-se de saudação tooanswer perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7579d-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="7579d-125">Os usuários de saudação estão familiarizados com autenticação multifator?</span><span class="sxs-lookup"><span data-stu-id="7579d-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="7579d-126">Alguns usos será uma autenticação adicional tooprovide necessário?</span><span class="sxs-lookup"><span data-stu-id="7579d-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="7579d-127">Se Sim, todos os Olá tempo, quando provenientes de redes externas, ou ao acessar aplicativos específicos, ou em outras condições?</span><span class="sxs-lookup"><span data-stu-id="7579d-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="7579d-128">Os usuários de saudação precisarão de treinamento sobre como toosetup e implementar a autenticação multifator?</span><span class="sxs-lookup"><span data-stu-id="7579d-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="7579d-129">Quais são os principais cenários de saudação que sua empresa deseja tooenable multi-factor authentication para seus usuários?</span><span class="sxs-lookup"><span data-stu-id="7579d-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="7579d-130">Depois de responder a perguntas anteriores de hello, será toounderstand capaz de se não houver autenticação multifator já foi implementado no local.</span><span class="sxs-lookup"><span data-stu-id="7579d-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="7579d-131">Essa avaliação é requisitos técnicos do hello toodefine importantes para configurar e habilitar os usuários de organizações Olá para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="7579d-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="7579d-132">Certifique-se de saudação tooanswer perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7579d-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="7579d-133">Sua empresa precisa de contas com privilégios de tooprotect com MFA?</span><span class="sxs-lookup"><span data-stu-id="7579d-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="7579d-134">Sua empresa precisa tooenable MFA para determinados aplicativos por motivos de conformidade?</span><span class="sxs-lookup"><span data-stu-id="7579d-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="7579d-135">Sua empresa precisa tooenable MFA para todos os usuários qualificados desses aplicativos ou somente administradores?</span><span class="sxs-lookup"><span data-stu-id="7579d-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="7579d-136">Você precisa tem MFA sempre habilitada ou somente quando os usuários de saudação estiverem conectados à sua rede corporativa?</span><span class="sxs-lookup"><span data-stu-id="7579d-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="7579d-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7579d-137">Next steps</span></span>
[<span data-ttu-id="7579d-138">Definir uma estratégia de adoção de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="7579d-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="7579d-139">Confira também</span><span class="sxs-lookup"><span data-stu-id="7579d-139">See also</span></span>
[<span data-ttu-id="7579d-140">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="7579d-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

