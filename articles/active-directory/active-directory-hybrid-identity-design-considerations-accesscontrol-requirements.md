---
title: "Considerações sobre design da identidade híbrida do Azure Active Directory - determinar os requisitos de controle de acesso | Microsoft Docs"
description: "Aborda os pilares da identidade e requisitos de acesso de identificação de recursos para usuários em um ambiente híbrido."
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
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="a3048-103">Determina os requisitos de controle de acesso para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="a3048-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="a3048-104">Quando uma organização está projetando sua solução de identidade híbrida, ela também pode usar essa oportunidade para examinar os requisitos de acesso para os recursos que pretende tornar disponível aos usuários.</span><span class="sxs-lookup"><span data-stu-id="a3048-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="a3048-105">O acesso a dados cruza todos os quatro pilares da identidade, que são:</span><span class="sxs-lookup"><span data-stu-id="a3048-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="a3048-106">Administração</span><span class="sxs-lookup"><span data-stu-id="a3048-106">Administration</span></span>
* <span data-ttu-id="a3048-107">Autenticação</span><span class="sxs-lookup"><span data-stu-id="a3048-107">Authentication</span></span>
* <span data-ttu-id="a3048-108">Autorização</span><span class="sxs-lookup"><span data-stu-id="a3048-108">Authorization</span></span>
* <span data-ttu-id="a3048-109">Auditoria</span><span class="sxs-lookup"><span data-stu-id="a3048-109">Auditing</span></span>

<span data-ttu-id="a3048-110">As seções a seguir abordarão a autenticação e a autorização com mais detalhes; a administração e a auditoria são parte do ciclo de vida da identidade híbrida.</span><span class="sxs-lookup"><span data-stu-id="a3048-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="a3048-111">Leia [Determinar as tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) para saber mais sobre esses recursos.</span><span class="sxs-lookup"><span data-stu-id="a3048-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="a3048-112">Leia [Os quatro pilares da identidade - gerenciamento de identidade na era da TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) para saber mais sobre cada um desses pilares.</span><span class="sxs-lookup"><span data-stu-id="a3048-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="a3048-113">Autenticação e autorização</span><span class="sxs-lookup"><span data-stu-id="a3048-113">Authentication and authorization</span></span>
<span data-ttu-id="a3048-114">Há cenários diferentes para autenticação e autorização; esses cenários terão requisitos específicos que devem ser atendidos pela solução de identidade híbrida que a empresa adotar.</span><span class="sxs-lookup"><span data-stu-id="a3048-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="a3048-115">Cenários que envolvem a comunicação entre empresas (B2B) podem representar um desafio adicional para administradores de TI, pois estes precisam garantir que os métodos de autenticação e autorização usados pela organização possam se comunicar com seus parceiros comerciais.</span><span class="sxs-lookup"><span data-stu-id="a3048-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="a3048-116">Durante o processo de criação de requisitos de autenticação e autorização, verifique se as seguintes perguntas são respondidas:</span><span class="sxs-lookup"><span data-stu-id="a3048-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="a3048-117">Sua organização irá autenticar e autorizar somente os usuários localizados em seu sistema de gerenciamento de identidade?</span><span class="sxs-lookup"><span data-stu-id="a3048-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="a3048-118">Há planos para cenários B2B?</span><span class="sxs-lookup"><span data-stu-id="a3048-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="a3048-119">Se sim, você já sabe quais protocolos (SAML, OAuth, Kerberos, Tokens ou Certificados) serão usados para conectar as duas empresas?</span><span class="sxs-lookup"><span data-stu-id="a3048-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="a3048-120">A solução de identidade híbrida que vocês vão adotar dá suporte a esses protocolos?</span><span class="sxs-lookup"><span data-stu-id="a3048-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="a3048-121">Outro ponto importante a considerar é onde o repositório de autenticação que será usado pelos usuários e parceiros estará localizado e o modelo administrativo que será usado.</span><span class="sxs-lookup"><span data-stu-id="a3048-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="a3048-122">Considere as duas opções principais a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3048-122">Consider the following two core options:</span></span>

* <span data-ttu-id="a3048-123">Centralizado: nesse modelo, as políticas, a administração e as credenciais do usuário podem ser centralizadas localmente ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3048-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="a3048-124">Híbrido: nesse modelo, as políticas, a administração e as credenciais do usuário serão centralizadas localmente e replicadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3048-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="a3048-125">Qual modelo sua organização adotará vai variar de acordo com suas necessidades de negócios. Responda às seguintes perguntas para identificar onde residirá o sistema de gerenciamento de identidade e o modo de uso administrativo:</span><span class="sxs-lookup"><span data-stu-id="a3048-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="a3048-126">Sua organização tem atualmente um gerenciamento de identidade local?</span><span class="sxs-lookup"><span data-stu-id="a3048-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="a3048-127">Se sim, ela pretende mantê-lo?</span><span class="sxs-lookup"><span data-stu-id="a3048-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="a3048-128">Há algum requisito de normas ou de conformidade que sua organização deve seguir que defina onde deve residir o sistema de gerenciamento de identidade?</span><span class="sxs-lookup"><span data-stu-id="a3048-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="a3048-129">Sua organização usa o logon único para aplicativos localizados no local ou na nuvem?</span><span class="sxs-lookup"><span data-stu-id="a3048-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="a3048-130">Em caso afirmativo, a adoção de um modelo de identidade híbrida afeta esse processo?</span><span class="sxs-lookup"><span data-stu-id="a3048-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="a3048-131">Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="a3048-131">Access Control</span></span>
<span data-ttu-id="a3048-132">Embora a autenticação e a autorização sejam os principais elementos para habilitar o acesso a dados corporativos usando a validação do usuário, também é importante controlar o nível de acesso que esses usuários terão e o nível de acesso que os administradores terão sobre os recursos que gerenciam.</span><span class="sxs-lookup"><span data-stu-id="a3048-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="a3048-133">Sua solução de identidade híbrida deve ser capaz de fornecer acesso granular ao controle de recursos, delegação e acesso à base de função.</span><span class="sxs-lookup"><span data-stu-id="a3048-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="a3048-134">Verifique se as seguintes perguntas são respondidas sobre o controle de acesso:</span><span class="sxs-lookup"><span data-stu-id="a3048-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="a3048-135">Sua empresa tem mais de um usuário com privilégio elevado para gerenciar seu sistema de identidade?</span><span class="sxs-lookup"><span data-stu-id="a3048-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="a3048-136">Em caso afirmativo, cada usuário precisa do mesmo nível de acesso?</span><span class="sxs-lookup"><span data-stu-id="a3048-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="a3048-137">Sua empresa precisa delegar acesso aos usuários para gerenciar recursos específicos?</span><span class="sxs-lookup"><span data-stu-id="a3048-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="a3048-138">Em caso afirmativo, com que frequência isso acontece?</span><span class="sxs-lookup"><span data-stu-id="a3048-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="a3048-139">Sua empresa precisa integrar os recursos de controle de acesso entre recursos locais e na nuvem?</span><span class="sxs-lookup"><span data-stu-id="a3048-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="a3048-140">Sua empresa precisa limitar o acesso aos recursos de acordo com algumas condições?</span><span class="sxs-lookup"><span data-stu-id="a3048-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="a3048-141">Sua empresa tem qualquer aplicativo que precise acessar alguns recursos de controle de acesso personalizado?</span><span class="sxs-lookup"><span data-stu-id="a3048-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="a3048-142">Em caso afirmativo, onde estão localizados os aplicativos (no local ou na nuvem)?</span><span class="sxs-lookup"><span data-stu-id="a3048-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="a3048-143">Em caso afirmativo, onde estão localizados os recursos de destino (no local ou na nuvem)?</span><span class="sxs-lookup"><span data-stu-id="a3048-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="a3048-144">Certifique-se de fazer anotações de cada resposta e entender o raciocínio por trás de resposta.</span><span class="sxs-lookup"><span data-stu-id="a3048-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="a3048-145">[Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) abordará as opções disponíveis e as vantagens/desvantagens de cada opção.</span><span class="sxs-lookup"><span data-stu-id="a3048-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="a3048-146">Depois de responder a essas perguntas, você selecionará a opção que melhor se ajusta às necessidades de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="a3048-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a3048-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3048-147">Next steps</span></span>
[<span data-ttu-id="a3048-148">Determinar requisitos de resposta a incidentes</span><span class="sxs-lookup"><span data-stu-id="a3048-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a3048-149">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a3048-149">See Also</span></span>
[<span data-ttu-id="a3048-150">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="a3048-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

