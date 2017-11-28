---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de gerenciamento de conteúdo | Microsoft Docs"
description: "Fornece informações sobre como toodetermine Olá requisitos de gerenciamento de conteúdo da sua empresa. Normalmente quando um usuário tem seu próprio dispositivo ele pode ter também várias credenciais que serão alternar o acordo aplicativo toohello que ele usa. É importante toodifferentiate o conteúdo que foi criado usando credenciais pessoais versus Olá aqueles criados usando credenciais corporativas. Sua solução de identidade deverá ser capaz de toointeract com tooprovide de serviços de nuvem uma experiência perfeita toohello final ao garantir sua privacidade e aumentar a proteção de saudação contra vazamento de dados."
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="702b4-106">Determinar os requisitos de gerenciamento de conteúdo para sua solução de identidade híbrida</span><span class="sxs-lookup"><span data-stu-id="702b4-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="702b4-107">Noções básicas sobre requisitos de gerenciamento de conteúdo de saudação para seu negócio pode direcionar afetam sua decisão sobre qual toouse de solução de identidade híbrida.</span><span class="sxs-lookup"><span data-stu-id="702b4-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="702b4-108">Com hello proliferação de vários dispositivos e a capacidade de saudação do usuários toobring seus próprios dispositivos ([BYOD](http://aka.ms/byodcg)), empresa Olá deve proteger seus próprios dados, mas ele também deve manter privacidade do usuário intacta.</span><span class="sxs-lookup"><span data-stu-id="702b4-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="702b4-109">Normalmente quando um usuário tem seu próprio dispositivo ele pode ter também várias credenciais que serão alternar o acordo aplicativo toohello que ele usa.</span><span class="sxs-lookup"><span data-stu-id="702b4-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="702b4-110">É importante toodifferentiate o conteúdo que foi criado usando credenciais pessoais versus Olá aqueles criados usando credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="702b4-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="702b4-111">Sua solução de identidade deverá ser capaz de toointeract com tooprovide de serviços de nuvem uma experiência perfeita toohello final ao garantir sua privacidade e aumentar a proteção de saudação contra vazamento de dados.</span><span class="sxs-lookup"><span data-stu-id="702b4-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="702b4-112">Sua solução de identidade será aproveitada por diferentes controles técnicos em gerenciamento de conteúdo do pedido tooprovide conforme mostrado na figura a saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="702b4-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="702b4-113">**Controles de segurança que aproveitarão o sistema de gerenciamento de identidade**</span><span class="sxs-lookup"><span data-stu-id="702b4-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="702b4-114">Em geral, os requisitos de gerenciamento de conteúdo utilizará seu sistema de gerenciamento de identidade no hello áreas a seguir:</span><span class="sxs-lookup"><span data-stu-id="702b4-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="702b4-115">Privacidade: identificação usuário Olá que possui um recurso e aplicar a integridade de toomaintain Olá controles apropriados.</span><span class="sxs-lookup"><span data-stu-id="702b4-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="702b4-116">Classificação de dados: identificar o usuário hello ou o grupo e o nível de objeto tooan de acesso de acordo com a classificação de tooits.</span><span class="sxs-lookup"><span data-stu-id="702b4-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="702b4-117">Proteção contra vazamento de dados: controles de segurança responsáveis por proteger vazamento de tooavoid dados precisará toointeract com identidade Olá identidade toovalidate saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="702b4-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="702b4-118">Isso também é importante para a finalidade de trilha de auditoria.</span><span class="sxs-lookup"><span data-stu-id="702b4-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="702b4-119">Leitura [classificação de dados para preparação de nuvem](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obter mais informações sobre as práticas recomendadas e diretrizes para a classificação de dados.</span><span class="sxs-lookup"><span data-stu-id="702b4-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="702b4-120">Ao planejar sua solução de identidade híbrida Certifique-se de que Olá a seguir são responder perguntas de acordo com os requisitos da organização tooyour:</span><span class="sxs-lookup"><span data-stu-id="702b4-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="702b4-121">Sua empresa tem controles de segurança em vigor tooenforce privacidade dos dados?</span><span class="sxs-lookup"><span data-stu-id="702b4-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="702b4-122">Em caso afirmativo, esses controles de segurança será capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?</span><span class="sxs-lookup"><span data-stu-id="702b4-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="702b4-123">Sua empresa usa a classificação de dados?</span><span class="sxs-lookup"><span data-stu-id="702b4-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="702b4-124">Em caso afirmativo, é Olá atual solução capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?</span><span class="sxs-lookup"><span data-stu-id="702b4-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="702b4-125">Sua empresa atualmente tem qualquer solução de vazamento de dados?</span><span class="sxs-lookup"><span data-stu-id="702b4-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="702b4-126">Em caso afirmativo, é Olá atual solução capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?</span><span class="sxs-lookup"><span data-stu-id="702b4-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="702b4-127">Sua empresa precisa tooaudit acesso tooresources?</span><span class="sxs-lookup"><span data-stu-id="702b4-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="702b4-128">Em caso afirmativo, que tipo de recursos?</span><span class="sxs-lookup"><span data-stu-id="702b4-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="702b4-129">Em caso afirmativo, qual nível de informação é necessário?</span><span class="sxs-lookup"><span data-stu-id="702b4-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="702b4-130">Em caso afirmativo, onde o log de auditoria Olá deve residir?</span><span class="sxs-lookup"><span data-stu-id="702b4-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="702b4-131">Local ou na nuvem Olá?</span><span class="sxs-lookup"><span data-stu-id="702b4-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="702b4-132">Sua empresa precisa tooencrypt qualquer e-mails que contenham dados confidenciais (CPFs, números de cartão de crédito, etc)?</span><span class="sxs-lookup"><span data-stu-id="702b4-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="702b4-133">Sua empresa precisa tooencrypt todos os documentos/conteúdo compartilhado com parceiros de negócios externos?</span><span class="sxs-lookup"><span data-stu-id="702b4-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="702b4-134">Sua empresa precisa de políticas corporativas de tooenforce em determinados tipos de emails (não responder a todos, não encaminhar)?</span><span class="sxs-lookup"><span data-stu-id="702b4-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="702b4-135">Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="702b4-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="702b4-136">[Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.</span><span class="sxs-lookup"><span data-stu-id="702b4-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="702b4-137">Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="702b4-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="702b4-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="702b4-138">Next steps</span></span>
[<span data-ttu-id="702b4-139">Determinar requisitos de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="702b4-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="702b4-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="702b4-140">See Also</span></span>
[<span data-ttu-id="702b4-141">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="702b4-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

