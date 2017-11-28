---
title: "Azure Active Directory B2C: Notas do desenvolvedor sobre o uso de políticas personalizadas | Microsoft Docs"
description: "Observações para os desenvolvedores sobre configuração e manutenção do B2C do Azure AD com políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="8fb00-103">Notas de versão para a versão prévia da política personalizada do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="8fb00-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="8fb00-104">Olá conjunto de recursos de política personalizada agora está disponível para avaliação em visualização pública para todos os Azure Active Directory B2C clientes (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="8fb00-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="8fb00-105">Esse conjunto de recursos é destinado a desenvolvedores de identidade avançado criando soluções de identidade hello mais complexas.</span><span class="sxs-lookup"><span data-stu-id="8fb00-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="8fb00-106">Atualmente, esse conjunto de recursos exige os desenvolvedores tooconfigure Olá identidade experiência Framework diretamente por meio da edição de arquivo XML.</span><span class="sxs-lookup"><span data-stu-id="8fb00-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="8fb00-107">Esse método de configuração é poderoso e complexo.</span><span class="sxs-lookup"><span data-stu-id="8fb00-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="8fb00-108">Os desenvolvedores de identidade usando Olá avançados Framework de experiência de identidade deve planejar tooinvest algum tempo para concluir o passo a passo e leitura de documentos de referência.</span><span class="sxs-lookup"><span data-stu-id="8fb00-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="8fb00-109">Recursos incluídos nesta versão prévia</span><span class="sxs-lookup"><span data-stu-id="8fb00-109">Features included in this public preview</span></span>
<span data-ttu-id="8fb00-110">Com hello novos recursos introduzidos na visualização pública hello, os desenvolvedores podem executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8fb00-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="8fb00-111">Criar e carregar percursos do usuário de autenticação personalizada usando políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8fb00-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="8fb00-112">Descrever percursos do usuário passo a passo como trocas entre provedores de declarações.</span><span class="sxs-lookup"><span data-stu-id="8fb00-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="8fb00-113">Definir a ramificação condicional em percursos do usuário.</span><span class="sxs-lookup"><span data-stu-id="8fb00-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="8fb00-114">Integrar os serviços habilitados para API REST aos seus percursos do usuário de autenticação personalizada.</span><span class="sxs-lookup"><span data-stu-id="8fb00-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="8fb00-115">Adicione a federação com provedores de identidade que são compatíveis com hello OpenIDConnect padrão.</span><span class="sxs-lookup"><span data-stu-id="8fb00-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="8fb00-116">Adicione a federação com provedores de identidade que seguem o protocolo toohello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="8fb00-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="8fb00-117">Termos de visualização pública Olá</span><span class="sxs-lookup"><span data-stu-id="8fb00-117">Terms of hello public preview</span></span>

* <span data-ttu-id="8fb00-118">Recomendamos que você toouse Olá novos recursos para fins de avaliação.</span><span class="sxs-lookup"><span data-stu-id="8fb00-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="8fb00-119">Os novos recursos não se destinam ao uso em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8fb00-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="8fb00-120">Contratos de nível de serviço (SLAs) não se aplicam a toohello novos recursos.</span><span class="sxs-lookup"><span data-stu-id="8fb00-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="8fb00-121">As solicitações de suporte podem ser arquivadas por meio dos canais de suporte normais.</span><span class="sxs-lookup"><span data-stu-id="8fb00-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="8fb00-122">Não há nenhuma data prometida para disponibilidade geral.</span><span class="sxs-lookup"><span data-stu-id="8fb00-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="8fb00-123">Nosso critério e por qualquer motivo, Microsoft pode sinalizar e rejeitar ou restringir cenários e Jornadas de usuário que excedem o escopo de saudação do hello Azure AD B2C produto compromisso tooserve como uma plataforma de gerenciamento (CIAM) de identidade e acesso de cliente.</span><span class="sxs-lookup"><span data-stu-id="8fb00-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="8fb00-124">Responsabilidades dos desenvolvedores de conjunto de recursos de política personalizada</span><span class="sxs-lookup"><span data-stu-id="8fb00-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="8fb00-125">Configuração da política manual concede acesso de nível inferior toohello subjacente a plataforma do Azure AD B2C e resulta na criação de saudação de uma estrutura de relação de confiança exclusivo e totalmente personalizável.</span><span class="sxs-lookup"><span data-stu-id="8fb00-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="8fb00-126">As possíveis permutações de provedores de identidade personalizado, relações de confiança, a integração com serviços externos e fluxos de trabalho passo a passo coloca demandas maiores no Olá avançado desenvolvedores consumi-las.</span><span class="sxs-lookup"><span data-stu-id="8fb00-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="8fb00-127">toofully vantagem da visualização pública do hello, sugerimos que os desenvolvedores utilizando o conjunto de recursos de política personalizada do hello aderem toohello diretrizes a seguir:</span><span class="sxs-lookup"><span data-stu-id="8fb00-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="8fb00-128">Familiarize-se com o idioma de configuração de saudação do hello mecanismo de experiência de identidade e gerenciamento de chave/segredos.</span><span class="sxs-lookup"><span data-stu-id="8fb00-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="8fb00-129">Apropriar-se de cenários e de integrações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8fb00-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="8fb00-130">Executar testes de cenário metódicos.</span><span class="sxs-lookup"><span data-stu-id="8fb00-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="8fb00-131">Siga as práticas recomendadas de desenvolvimento/preparo de software com no mínimo um ambiente de desenvolvimento e teste um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8fb00-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="8fb00-132">Se mantenha informado sobre novos desenvolvimentos de provedores de identidade hello e integrar com os serviços.</span><span class="sxs-lookup"><span data-stu-id="8fb00-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="8fb00-133">Por exemplo, manter controle das alterações no segredos e do serviço de toohello programado e alterações.</span><span class="sxs-lookup"><span data-stu-id="8fb00-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="8fb00-134">Configurar o monitoramento ativo e monitorar a capacidade de resposta de saudação de ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="8fb00-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="8fb00-135">Manter os endereços de email de contato atuais e permanecer emails de site live equipe Microsoft toohello responsivo.</span><span class="sxs-lookup"><span data-stu-id="8fb00-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="8fb00-136">Agir em tempo hábil quando toodo aconselhado Olá isso, a equipe do Microsoft live-site.</span><span class="sxs-lookup"><span data-stu-id="8fb00-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="8fb00-137">Esses recursos eventualmente podem ser incluídos nas políticas internas do AD do Azure, tornando-os desenvolvedores de tooall mais acessíveis.</span><span class="sxs-lookup"><span data-stu-id="8fb00-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fb00-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fb00-138">Next steps</span></span>
<span data-ttu-id="8fb00-139">[Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8fb00-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
