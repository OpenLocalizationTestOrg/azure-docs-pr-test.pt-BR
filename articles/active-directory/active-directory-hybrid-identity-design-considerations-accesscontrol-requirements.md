---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de controle de acesso | Microsoft Docs"
description: "Abrange Olá colunas de identidade e identificação de requisitos de acesso para recursos para usuários em um ambiente híbrido."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="d0b4b-103">Determina os requisitos de controle de acesso para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="d0b4b-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="d0b4b-104">Durante a criação de uma organização sua solução de identidade híbrida eles também podem usar esta oportunidade tooreview acessar requisitos para recursos de saudação que estão planejando toomake disponível para os usuários.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-104">When an organization is designing their hybrid identity solution they can also use this opportunity tooreview access requirements for hello resources that they are planning toomake it available for users.</span></span> <span data-ttu-id="d0b4b-105">acesso a dados Olá cruzada todas as quatro colunas de identidade, que são:</span><span class="sxs-lookup"><span data-stu-id="d0b4b-105">hello data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="d0b4b-106">Administração</span><span class="sxs-lookup"><span data-stu-id="d0b4b-106">Administration</span></span>
* <span data-ttu-id="d0b4b-107">Autenticação</span><span class="sxs-lookup"><span data-stu-id="d0b4b-107">Authentication</span></span>
* <span data-ttu-id="d0b4b-108">Autorização</span><span class="sxs-lookup"><span data-stu-id="d0b4b-108">Authorization</span></span>
* <span data-ttu-id="d0b4b-109">Auditoria</span><span class="sxs-lookup"><span data-stu-id="d0b4b-109">Auditing</span></span>

<span data-ttu-id="d0b4b-110">seções de saudação que segue abordará autenticação e autorização em mais detalhes, administração e a auditoria são parte do ciclo de vida de identidade híbrida hello.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-110">hello sections that follows will cover authentication and authorization in more details, administration and auditing are part of hello hybrid identity lifecycle.</span></span> <span data-ttu-id="d0b4b-111">Leia [Determinar as tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) para saber mais sobre esses recursos.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="d0b4b-112">Leitura [Olá quatro colunas de identidade - gerenciamento de identidade no hello idade de TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) para obter mais informações sobre cada um dessas colunas.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-112">Read [hello Four Pillars of Identity - Identity Management in hello Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="d0b4b-113">Autenticação e autorização</span><span class="sxs-lookup"><span data-stu-id="d0b4b-113">Authentication and authorization</span></span>
<span data-ttu-id="d0b4b-114">Há cenários diferentes para autenticação e autorização, esses cenários terá requisitos específicos que devem ser atendidos pela solução de identidade híbrida Olá empresa Olá é tooadopt contínuo.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by hello hybrid identity solution that hello company is going tooadopt.</span></span> <span data-ttu-id="d0b4b-115">Cenários que envolvem tooBusiness Business (B2B) comunicação pode adicionar um desafio extra para administradores de TI desde que eles precisarão tooensure que método de autenticação e autorização de hello usado pela organização Olá pode se comunicar com seus parceiros comerciais.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-115">Scenarios involving Business tooBusiness (B2B) communication can add an extra challenge for IT Admins since they will need tooensure that hello authentication and authorization method used by hello organization can communicate with their business partners.</span></span> <span data-ttu-id="d0b4b-116">Durante a saudação criar processo para obter os requisitos de autenticação e autorização, certifique-se de que Olá perguntas a seguir são atendidos:</span><span class="sxs-lookup"><span data-stu-id="d0b4b-116">During hello designing process for authentication and authorization requirements, ensure that hello following questions are answered:</span></span>

* <span data-ttu-id="d0b4b-117">Sua organização irá autenticar e autorizar somente os usuários localizados em seu sistema de gerenciamento de identidade?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="d0b4b-118">Há planos para cenários B2B?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="d0b4b-119">Se Sim, você já sabe quais protocolos (SAML, OAuth, Kerberos, Tokens ou certificados) serão ser usado tooconnect ambas as empresas?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used tooconnect both businesses?</span></span>
* <span data-ttu-id="d0b4b-120">Solução de identidade híbrida Olá vai tooadopt dá suporte a esses protocolos?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-120">Does hello hybrid identity solution that you are going tooadopt support those protocols?</span></span>

<span data-ttu-id="d0b4b-121">Outro tooconsider ponto importante é onde o repositório de autenticação de saudação que será usado por parceiros e usuários estarão localizado e toobe de modelo administrativo Olá usado.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-121">Another important point tooconsider is where hello authentication repository that will be used by users and partners will be located and hello administrative model toobe used.</span></span> <span data-ttu-id="d0b4b-122">Considere Olá duas opções principais a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0b4b-122">Consider hello following two core options:</span></span>

* <span data-ttu-id="d0b4b-123">Centralizado: em Olá esse modelo credenciais do usuário, políticas e administração podem ser centralizado local ou na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-123">Centralized: in this model hello user’s credentials, policies and administration can be centralized on-premises or in hello cloud.</span></span>
* <span data-ttu-id="d0b4b-124">Híbrido: em Olá esse modelo credenciais do usuário, políticas e administração será centralizado local e um replicadas na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-124">Hybrid: in this model hello user’s credentials, policies and administration will be centralized on-premises and a replicated in hello cloud.</span></span>

<span data-ttu-id="d0b4b-125">Qual modelo de sua organização adotarão irá variar de acordo requisitos de negócios tootheir, você deseja tooanswer Olá tooidentify perguntas em que o sistema de gerenciamento de identidade Olá residirá e Olá toouse do modo de administrador a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0b4b-125">Which model your organization will adopt will vary according tootheir business requirements, you want tooanswer hello following questions tooidentify where hello identity management system will reside and hello administrative mode toouse:</span></span>

* <span data-ttu-id="d0b4b-126">Sua organização tem atualmente um gerenciamento de identidade local?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="d0b4b-127">Em caso afirmativo, eles planejam tookeep-lo?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-127">If yes, do they plan tookeep it?</span></span>
  * <span data-ttu-id="d0b4b-128">Há algum requisito de conformidade ou regulamentação que sua organização deve seguir que impõe qual sistema de gerenciamento de identidade Olá deve residir?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-128">Are there any regulation or compliance requirements that your organization must follow that dictates where hello identity management system should reside?</span></span>
* <span data-ttu-id="d0b4b-129">Sua organização usar o logon único para aplicativos localizados no local ou na nuvem Olá?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-129">Does your organization use single sign-on for apps located on-premises or in hello cloud?</span></span>
  * <span data-ttu-id="d0b4b-130">Em caso afirmativo, a adoção de saudação de um modelo de identidade híbrida afeta esse processo?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-130">If yes, does hello adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="d0b4b-131">Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="d0b4b-131">Access Control</span></span>
<span data-ttu-id="d0b4b-132">Enquanto a autenticação e autorização são os principais elementos tooenable acessar toocorporate dados por meio da validação do usuário, também é importante toocontrol nível de saudação de acesso que esses usuários terão e nível de saudação de administradores de acesso terá sobre Olá recursos que estão gerenciando.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-132">While authentication and authorization are core elements tooenable access toocorporate data through user’s validation, it is also important toocontrol hello level of access that these users will have and hello level of access administrators will have over hello resources that they are managing.</span></span> <span data-ttu-id="d0b4b-133">Sua solução de identidade híbrida deve ser capaz de tooprovide acesso granular tooresources, controle de acesso de base de função e delegação.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-133">Your hybrid identity solution must be able tooprovide granular access tooresources, delegation and role base access control.</span></span> <span data-ttu-id="d0b4b-134">Certifique-se de que Olá pergunta a seguir são respondidas sobre controle de acesso:</span><span class="sxs-lookup"><span data-stu-id="d0b4b-134">Ensure that hello following question are answered regarding access control:</span></span>

* <span data-ttu-id="d0b4b-135">Sua empresa tem mais de um usuário com privilégios elevados toomanage seu sistema de identidade?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-135">Does your company have more than one user with elevated privilege toomanage your identity system?</span></span>
  * <span data-ttu-id="d0b4b-136">Se Sim, cada usuário precisar Olá nível mesmo de acesso?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-136">If yes, does each user need hello same access level?</span></span>
* <span data-ttu-id="d0b4b-137">Seria necessário toodelegate acesso toousers toomanage específico recursos de sua empresa?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-137">Would your company need toodelegate access toousers toomanage specific resources?</span></span>
  * <span data-ttu-id="d0b4b-138">Em caso afirmativo, com que frequência isso acontece?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="d0b4b-139">Sua empresa precisaria toointegrate recursos de controle de acesso entre local e nuvem recursos?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-139">Would your company need toointegrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="d0b4b-140">Sua empresa precisaria toolimit tooresources de acesso de acordo com as condições de toosome?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-140">Would your company need toolimit access tooresources according toosome conditions?</span></span>
* <span data-ttu-id="d0b4b-141">Sua empresa teria qualquer aplicativo que precisa acessar toosome recursos de controle personalizado?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-141">Would your company have any application that needs custom control access toosome resources?</span></span>
  * <span data-ttu-id="d0b4b-142">Em caso afirmativo, esses aplicativos localização (local ou na nuvem Olá)?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-142">If yes, where are those apps located (on-premises or in hello cloud)?</span></span>
  * <span data-ttu-id="d0b4b-143">Em caso afirmativo, onde estão os recursos de destino localizados (local ou na nuvem Olá)?</span><span class="sxs-lookup"><span data-stu-id="d0b4b-143">If yes, where are those target resources located (on-premises or in hello cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="d0b4b-144">Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-144">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="d0b4b-145">[Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="d0b4b-146">Depois de responder a essas perguntas, você selecionará a opção que melhor se ajusta às necessidades de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="d0b4b-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d0b4b-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0b4b-147">Next steps</span></span>
[<span data-ttu-id="d0b4b-148">Determinar requisitos de resposta a incidentes</span><span class="sxs-lookup"><span data-stu-id="d0b4b-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="d0b4b-149">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d0b4b-149">See Also</span></span>
[<span data-ttu-id="d0b4b-150">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="d0b4b-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

