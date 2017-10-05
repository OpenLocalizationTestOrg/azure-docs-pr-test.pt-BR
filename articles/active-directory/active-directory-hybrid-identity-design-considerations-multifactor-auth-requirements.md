---
title: "Considerações sobre design da identidade híbrida do Active Directory do Azure - determinar os requisitos da autenticação multifator"
description: "Com o controle de acesso condicional, o Active Directory do Azure verifica as condições específicas escolhidas para autenticação do usuário, antes de permitir o acesso ao aplicativo. Quando essas condições forem atendidas, o usuário é autenticado e autorizado a acessar o aplicativo."
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
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="697ae-104">Determinar os requisitos de autenticação multifator para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="697ae-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="697ae-105">Em um mundo de mobilidade, com os usuários que acessam dados e aplicativos na nuvem e de qualquer dispositivo, proteger essas informações tornou imprescindível.</span><span class="sxs-lookup"><span data-stu-id="697ae-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="697ae-106">Todos os dias há um novo título sobre violação de segurança.</span><span class="sxs-lookup"><span data-stu-id="697ae-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="697ae-107">No entanto, não há nenhuma garantia contra falhas desse tipo, a autenticação multifator, fornece uma camada adicional de segurança para ajudar a evitar essas violações.</span><span class="sxs-lookup"><span data-stu-id="697ae-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="697ae-108">Comece pela avaliação das necessidades de organizações para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="697ae-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="697ae-109">Ou seja, o que a organização está tentando proteger.</span><span class="sxs-lookup"><span data-stu-id="697ae-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="697ae-110">Essa avaliação é importante para definir os requisitos técnicos para configurar e habilitar os usuários de organizações para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="697ae-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="697ae-111">Se você não estiver familiarizado com o MFA e o que ele faz, é altamente recomendável que você leia o artigo [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) antes de continuar a ler esta seção.</span><span class="sxs-lookup"><span data-stu-id="697ae-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="697ae-112">Certifique-se de responder ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="697ae-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="697ae-113">Sua empresa está tentando proteger aplicativos Microsoft?</span><span class="sxs-lookup"><span data-stu-id="697ae-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="697ae-114">Como esses aplicativos são publicados?</span><span class="sxs-lookup"><span data-stu-id="697ae-114">How these apps are published?</span></span>
* <span data-ttu-id="697ae-115">Sua empresa oferecer acesso remoto para permitir que os funcionários acessem aplicativos locais?</span><span class="sxs-lookup"><span data-stu-id="697ae-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="697ae-116">Em caso afirmativo, que tipo de acesso remoto? Você também precisa avaliar onde os usuários que estiverem acessando esses aplicativos estarão.</span><span class="sxs-lookup"><span data-stu-id="697ae-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="697ae-117">Essa avaliação é outro passo importante para definir a estratégia de autenticação multifator adequada.</span><span class="sxs-lookup"><span data-stu-id="697ae-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="697ae-118">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="697ae-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="697ae-119">Onde os usuários estarão?</span><span class="sxs-lookup"><span data-stu-id="697ae-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="697ae-120">Podem ser localizados em qualquer lugar?</span><span class="sxs-lookup"><span data-stu-id="697ae-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="697ae-121">Sua empresa deseja estabelecer restrições de acordo com a localização do usuário?</span><span class="sxs-lookup"><span data-stu-id="697ae-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="697ae-122">Depois de compreender esses requisitos, é importante também avaliar os requisitos do usuário para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="697ae-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="697ae-123">Essa avaliação é importante que porque definirá os requisitos para implantaram uma autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="697ae-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="697ae-124">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="697ae-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="697ae-125">O s usuários estão familiarizados com a autenticação multifator?</span><span class="sxs-lookup"><span data-stu-id="697ae-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="697ae-126">Alguns usos serão necessários para fornecer autenticação adicional?</span><span class="sxs-lookup"><span data-stu-id="697ae-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="697ae-127">Em caso afirmativo, o tempo todo, quando se originar de redes externas ou acessar aplicativos específicos ou em outras condições?</span><span class="sxs-lookup"><span data-stu-id="697ae-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="697ae-128">Os usuários exigirão treinamento sobre como configurar e implementar a autenticação multifator?</span><span class="sxs-lookup"><span data-stu-id="697ae-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="697ae-129">Quais são os cenários principais que sua empresa quer habilitar a autenticação multifator para seus usuários?</span><span class="sxs-lookup"><span data-stu-id="697ae-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="697ae-130">Depois de responder às perguntas anteriores, você poderá determinar se há autenticação multifator já implementada localmente.</span><span class="sxs-lookup"><span data-stu-id="697ae-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="697ae-131">Essa avaliação é importante para definir os requisitos técnicos para configurar e habilitar os usuários de organizações para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="697ae-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="697ae-132">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="697ae-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="697ae-133">Sua empresa precisa proteger contas privilegiadas com MFA?</span><span class="sxs-lookup"><span data-stu-id="697ae-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="697ae-134">Sua empresa precisa habilitar a MFA para determinado aplicativo por motivos de conformidade?</span><span class="sxs-lookup"><span data-stu-id="697ae-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="697ae-135">Sua empresa precisa habilitar a MFA para todos os usuários qualificados desses aplicativos ou apenas os administradores?</span><span class="sxs-lookup"><span data-stu-id="697ae-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="697ae-136">Você precisa ter o MFA sempre habilitado ou somente quando os usuários estão conectados fora da rede corporativa?</span><span class="sxs-lookup"><span data-stu-id="697ae-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="697ae-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="697ae-137">Next steps</span></span>
[<span data-ttu-id="697ae-138">Definir uma estratégia de adoção de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="697ae-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="697ae-139">Confira também</span><span class="sxs-lookup"><span data-stu-id="697ae-139">See also</span></span>
[<span data-ttu-id="697ae-140">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="697ae-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

