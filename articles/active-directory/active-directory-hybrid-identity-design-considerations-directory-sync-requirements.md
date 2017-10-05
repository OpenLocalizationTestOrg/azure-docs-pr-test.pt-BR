---
title: "Considerações sobre o design da identidade híbrida do Azure Active Directory - determinar os requisitos de sincronização de diretório | Microsoft Docs"
description: "Identificar quais requisitos são necessários para a sincronização de todos os usuários entre nos locais e nuvem para a empresa."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="4496b-103">Determinar os requisitos de sincronização de diretório</span><span class="sxs-lookup"><span data-stu-id="4496b-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="4496b-104">Sincronização é fornecer aos usuários uma identidade na nuvem com base em sua identidade local.</span><span class="sxs-lookup"><span data-stu-id="4496b-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="4496b-105">Em caso positivo ou negativo, usarão a conta sincronizada para autenticação ou autenticação federada, os usuários ainda precisarão ter uma identidade na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4496b-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="4496b-106">Essa identidade precisará ser mantida e atualizada periodicamente.</span><span class="sxs-lookup"><span data-stu-id="4496b-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="4496b-107">As atualizações podem ter várias formas, desde alterações de título para alterações de senha.</span><span class="sxs-lookup"><span data-stu-id="4496b-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="4496b-108">Comece avaliando a solução de identidade local das organizações e requisitos de usuário.</span><span class="sxs-lookup"><span data-stu-id="4496b-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="4496b-109">Essa avaliação é importante para definir os requisitos técnicos para como as identidades de usuário serão criadas e mantidas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4496b-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="4496b-110">Para a maioria das organizações, o Active Directory está local e será o diretório local que os usuários serão por sincronizado, porém em alguns casos este não será o caso.</span><span class="sxs-lookup"><span data-stu-id="4496b-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="4496b-111">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="4496b-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="4496b-112">Você tem uma floresta do AD, várias ou nenhuma?</span><span class="sxs-lookup"><span data-stu-id="4496b-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="4496b-113">Quantos diretórios AD do Azure você vai sincronizar?</span><span class="sxs-lookup"><span data-stu-id="4496b-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="4496b-114">Você está usando a filtragem?</span><span class="sxs-lookup"><span data-stu-id="4496b-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="4496b-115">Você tem vários servidores do Azure AD Connect planejados?</span><span class="sxs-lookup"><span data-stu-id="4496b-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="4496b-116">Atualmente, você tem uma ferramenta de sincronização local?</span><span class="sxs-lookup"><span data-stu-id="4496b-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="4496b-117">Em caso positivo, os usuários têm um diretório virtual/integração das identidades?</span><span class="sxs-lookup"><span data-stu-id="4496b-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="4496b-118">Você tem qualquer outro diretório local que deseja sincronizar (por exemplo, diretório LDAP, banco de dados de RH, etc)?</span><span class="sxs-lookup"><span data-stu-id="4496b-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="4496b-119">Você vai fazer qualquer GALSync?</span><span class="sxs-lookup"><span data-stu-id="4496b-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="4496b-120">O que é o estado atual do UPNs na sua organização?</span><span class="sxs-lookup"><span data-stu-id="4496b-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="4496b-121">Você tem um diretório diferente que os usuários se autenticam?</span><span class="sxs-lookup"><span data-stu-id="4496b-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="4496b-122">Sua empresa usa o Microsoft Exchange?</span><span class="sxs-lookup"><span data-stu-id="4496b-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="4496b-123">Planeja de ter uma implantação híbrida de mudança?</span><span class="sxs-lookup"><span data-stu-id="4496b-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="4496b-124">Agora que você tem uma ideia sobre os requisitos de sincronização, será necessário determinar qual ferramenta é a correta para atender a esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="4496b-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="4496b-125">A Microsoft fornece várias ferramentas para realizar a integração e a sincronização de diretórios.</span><span class="sxs-lookup"><span data-stu-id="4496b-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="4496b-126">Consulte [Tabela de comparação das ferramentas de integração de diretórios de Identidade Híbrida](active-directory-hybrid-identity-design-considerations-tools-comparison.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="4496b-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="4496b-127">Agora que você tem uma ideia sobre os requisitos de sincronização para a sua empresa, será necessário avaliar os aplicativos que usam esses serviços de diretório.</span><span class="sxs-lookup"><span data-stu-id="4496b-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="4496b-128">Essa avaliação é importante para definir os requisitos técnicos para integrar esses aplicativos para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="4496b-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="4496b-129">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="4496b-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="4496b-130">Esses aplicativos serão movidos para a nuvem e usar o diretório?</span><span class="sxs-lookup"><span data-stu-id="4496b-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="4496b-131">Há atributos especiais que precisam ser sincronizados na nuvem para que esses aplicativos possam usá-los com sucesso?</span><span class="sxs-lookup"><span data-stu-id="4496b-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="4496b-132">Esses aplicativos precisarão ser reescritos para tirar proveito da autenticação da nuvem?</span><span class="sxs-lookup"><span data-stu-id="4496b-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="4496b-133">Esses aplicativos continuarão a permanecer local enquanto os usuários os acessam usando a identidade de nuvem?</span><span class="sxs-lookup"><span data-stu-id="4496b-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="4496b-134">Você também precisa determinar a sincronização de diretórios de requisitos e restrições de segurança.</span><span class="sxs-lookup"><span data-stu-id="4496b-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="4496b-135">Essa avaliação é importante para obter uma lista dos requisitos que serão necessários para criar e manter as identidades do usuário na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4496b-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="4496b-136">Certifique-se de responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="4496b-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="4496b-137">Onde o servidor de sincronização estará?</span><span class="sxs-lookup"><span data-stu-id="4496b-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="4496b-138">Será integrado ao domínio?</span><span class="sxs-lookup"><span data-stu-id="4496b-138">Will it be domain joined?</span></span>
* <span data-ttu-id="4496b-139">O servidor será localizado em uma rede restrita por trás de um firewall, como um DMZ?</span><span class="sxs-lookup"><span data-stu-id="4496b-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="4496b-140">Você poderá abrir as portas de firewall necessárias para dar suporte à sincronização?</span><span class="sxs-lookup"><span data-stu-id="4496b-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="4496b-141">Você tem um plano de recuperação de desastres para o servidor de sincronização?</span><span class="sxs-lookup"><span data-stu-id="4496b-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="4496b-142">Você tem uma conta com as permissões corretas para todas as florestas que deseja sincronizar?</span><span class="sxs-lookup"><span data-stu-id="4496b-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="4496b-143">Se sua empresa não sabe a resposta para essa pergunta, leia a seção "Permissões de sincronização de senha" no artigo [Instalar o serviço de sincronização do Active Directory do Azure](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) e determine se você já tiver uma conta com essas permissões, ou se você precisar criar uma.</span><span class="sxs-lookup"><span data-stu-id="4496b-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="4496b-144">Se você tiver sincronização multi-floresta o servidor de sincronização é capaz de obter em cada floresta?</span><span class="sxs-lookup"><span data-stu-id="4496b-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="4496b-145">Certifique-se de fazer anotações de cada resposta e entender o raciocínio por trás de resposta.</span><span class="sxs-lookup"><span data-stu-id="4496b-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="4496b-146">[Determinar os requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) vai ultrapassar as opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4496b-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="4496b-147">Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="4496b-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4496b-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4496b-148">Next steps</span></span>
[<span data-ttu-id="4496b-149">Determinar os requisitos de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="4496b-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="4496b-150">Confira também</span><span class="sxs-lookup"><span data-stu-id="4496b-150">See also</span></span>
[<span data-ttu-id="4496b-151">Visão geral sobre as considerações de design</span><span class="sxs-lookup"><span data-stu-id="4496b-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

