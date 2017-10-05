---
title: "Considerações de design da identidade híbrida do Azure Active Directory - determinar os requisitos de gerenciamento de conteúdo | Microsoft Docs"
description: "Fornece informações sobre como determinar os requisitos de gerenciamento de conteúdo da sua empresa. Normalmente quando o usuário tem seu próprio dispositivo, ele terá também várias credenciais que serão alternadas de acordo com o aplicativo que usa. É importante diferenciar o conteúdo que foi criado usando credenciais pessoais em comparação com aquelas criadas usando credenciais corporativas. Sua solução de identidade deve ser capaz de interagir com os serviços de nuvem para fornecer uma experiência perfeita ao usuário final ao garantir a sua privacidade e aumentar a proteção contra a perda de dados."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="23fab-106">Determinar os requisitos de gerenciamento de conteúdo para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="23fab-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="23fab-107">Noções básicas sobre os requisitos de gerenciamento de conteúdo para a sua empresa direta podem afetar sua decisão sobre qual solução de identidade híbrida usar.</span><span class="sxs-lookup"><span data-stu-id="23fab-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="23fab-108">Com a proliferação de vários dispositivos e a capacidade dos usuários para levar seus próprios dispositivos ([BYOD](http://aka.ms/byodcg)), a empresa precisa proteger seus próprios dados, mas também deve manter a privacidade do usuário intacta.</span><span class="sxs-lookup"><span data-stu-id="23fab-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="23fab-109">Normalmente quando o usuário tem seu próprio dispositivo, ele terá também várias credenciais que serão alternadas de acordo com o aplicativo que usa.</span><span class="sxs-lookup"><span data-stu-id="23fab-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="23fab-110">É importante diferenciar o conteúdo que foi criado usando credenciais pessoais em comparação com aquelas criadas usando credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="23fab-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="23fab-111">Sua solução de identidade deve ser capaz de interagir com os serviços de nuvem para fornecer uma experiência perfeita ao usuário final ao garantir a sua privacidade e aumentar a proteção contra a perda de dados.</span><span class="sxs-lookup"><span data-stu-id="23fab-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="23fab-112">Sua solução de identidade será aproveitada por controles de técnicos diferentes para fornecer gerenciamento de conteúdo, como mostrado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="23fab-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="23fab-113">**Controles de segurança que aproveitarão o sistema de gerenciamento de identidade**</span><span class="sxs-lookup"><span data-stu-id="23fab-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="23fab-114">Em geral, os requisitos de gerenciamento de conteúdo aproveitará o sistema de gerenciamento de identidade nas seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="23fab-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="23fab-115">Privacidade: identificação do usuário que possui um recurso e aplica os controles apropriados para manter a integridade.</span><span class="sxs-lookup"><span data-stu-id="23fab-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="23fab-116">Classificação de dados: identificar o usuário ou grupo e nível de acesso a um objeto de acordo com sua classificação.</span><span class="sxs-lookup"><span data-stu-id="23fab-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="23fab-117">Proteção contra vazamento de dados: controles de segurança responsáveis pela proteção de dados para evitar vazamento precisam interagir com o sistema de identidade para validar a identidade do usuário.</span><span class="sxs-lookup"><span data-stu-id="23fab-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="23fab-118">Isso também é importante para a finalidade de trilha de auditoria.</span><span class="sxs-lookup"><span data-stu-id="23fab-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="23fab-119">Leitura [classificação de dados para preparação de nuvem](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obter mais informações sobre as práticas recomendadas e diretrizes para a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="23fab-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="23fab-120">Quando planejar sua solução de identidade híbrida, certifique-se de que as seguintes perguntas serão respondidas de acordo com os requisitos da sua organização:</span><span class="sxs-lookup"><span data-stu-id="23fab-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="23fab-121">Sua empresa tem controles de segurança ativos para aplicar a privacidade dos dados?</span><span class="sxs-lookup"><span data-stu-id="23fab-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="23fab-122">Em caso positivo, esses controles de segurança poderão integrar com a solução de identidade híbrida que você vai adotar?</span><span class="sxs-lookup"><span data-stu-id="23fab-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="23fab-123">Sua empresa usa a classificação de dados?</span><span class="sxs-lookup"><span data-stu-id="23fab-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="23fab-124">Em caso positivo, a solução atual é capaz de se integrar com a solução de identidade híbrida que você vai adotar?</span><span class="sxs-lookup"><span data-stu-id="23fab-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="23fab-125">Sua empresa atualmente tem qualquer solução de vazamento de dados?</span><span class="sxs-lookup"><span data-stu-id="23fab-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="23fab-126">Em caso positivo, a solução atual é capaz de se integrar com a solução de identidade híbrida que você vai adotar?</span><span class="sxs-lookup"><span data-stu-id="23fab-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="23fab-127">Sua empresa precisa auditar o acesso a recursos?</span><span class="sxs-lookup"><span data-stu-id="23fab-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="23fab-128">Em caso afirmativo, que tipo de recursos?</span><span class="sxs-lookup"><span data-stu-id="23fab-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="23fab-129">Em caso afirmativo, qual nível de informação é necessário?</span><span class="sxs-lookup"><span data-stu-id="23fab-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="23fab-130">Em caso afirmativo, onde o log de auditoria deve residir?</span><span class="sxs-lookup"><span data-stu-id="23fab-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="23fab-131">Local ou na nuvem?</span><span class="sxs-lookup"><span data-stu-id="23fab-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="23fab-132">Sua empresa precisa criptografar qualquer email que contêm dados confidenciais (SSNs, números de cartão de crédito, etc)?</span><span class="sxs-lookup"><span data-stu-id="23fab-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="23fab-133">Sua empresa precisa criptografar todos os documentos/conteúdos compartilhados com parceiros comerciais externos?</span><span class="sxs-lookup"><span data-stu-id="23fab-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="23fab-134">Sua empresa precisa impor políticas corporativas em determinados tipos de emails (não responder a todos, não encaminhar)?</span><span class="sxs-lookup"><span data-stu-id="23fab-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="23fab-135">Certifique-se de fazer anotações de cada resposta e entender o raciocínio por trás de resposta.</span><span class="sxs-lookup"><span data-stu-id="23fab-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="23fab-136">[Definir a estratégia de proteção de dados definir](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) ultrapassará as opções disponíveis e vantagens/desvantagens de cada opção.</span><span class="sxs-lookup"><span data-stu-id="23fab-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="23fab-137">Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="23fab-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="23fab-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23fab-138">Next steps</span></span>
[<span data-ttu-id="23fab-139">Determinar requisitos de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="23fab-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="23fab-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="23fab-140">See Also</span></span>
[<span data-ttu-id="23fab-141">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="23fab-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

