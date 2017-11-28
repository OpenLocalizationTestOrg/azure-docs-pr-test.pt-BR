---
title: dados pessoais de aaaProtect no Microsoft Azure | Microsoft Docs
description: "Primeiro artigo em uma série de artigos toohelp você usar dados pessoais tooprotect do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="aaf5b-103">Proteger dados pessoais no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="aaf5b-104">Este artigo apresenta uma série de artigos que ajudarão a usar a segurança do Azure tecnologias e serviços tooprotect dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="aaf5b-105">Este é um requisito fundamental para muitas iniciativas de governança e conformidade corporativas e do setor.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="aaf5b-106">cenário de Hello, metas de instrução e da empresa do problema são incluídas aqui.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="aaf5b-107">Cenário e declaração do problema</span><span class="sxs-lookup"><span data-stu-id="aaf5b-107">Scenario and problem statement</span></span>

<span data-ttu-id="aaf5b-108">Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="aaf5b-109">toosupport os esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK</span><span class="sxs-lookup"><span data-stu-id="aaf5b-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="aaf5b-110">empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="aaf5b-111">Isso pode incluir funcionário e/ou informações do cliente, como:</span><span class="sxs-lookup"><span data-stu-id="aaf5b-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="aaf5b-112">endereços</span><span class="sxs-lookup"><span data-stu-id="aaf5b-112">addresses</span></span>
- <span data-ttu-id="aaf5b-113">números de telefone</span><span class="sxs-lookup"><span data-stu-id="aaf5b-113">phone numbers</span></span>
- <span data-ttu-id="aaf5b-114">números de identificação fiscal</span><span class="sxs-lookup"><span data-stu-id="aaf5b-114">tax identification numbers</span></span>
- <span data-ttu-id="aaf5b-115">informações de médicas</span><span class="sxs-lookup"><span data-stu-id="aaf5b-115">medical information</span></span>
- <span data-ttu-id="aaf5b-116">informações de cartão de crédito</span><span class="sxs-lookup"><span data-stu-id="aaf5b-116">credit card information</span></span>

<span data-ttu-id="aaf5b-117">empresa Olá deve proteger a privacidade de Olá do funcionário e dados do cliente ao fazer departamentos toothose acessível de dados que precisam dela.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="aaf5b-118">(como departamentos de folha de pagamento e reservas)</span><span class="sxs-lookup"><span data-stu-id="aaf5b-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="aaf5b-119">Metas da empresa</span><span class="sxs-lookup"><span data-stu-id="aaf5b-119">Company goals</span></span> 

- <span data-ttu-id="aaf5b-120">As fontes de dados que contêm dados pessoais são criptografadas quando residem no armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="aaf5b-121">Dados pessoais que são transferidos de um local tooanother são criptografados ao mesmo tempo em trânsito.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="aaf5b-122">Isso é verdadeiro se dados saudação está viajando em rede virtual hello ou Olá Internet entre o datacenter corporativo hello e hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="aaf5b-123">A confidencialidade e a integridade dos dados pessoais são protegidas contra o acesso não autorizado por tecnologias de controle de acesso e gerenciamento de identidade forte.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="aaf5b-124">Os dados pessoais são protegidos contra a exposição por meio da violação de dados com o monitoramento de ameaças e vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="aaf5b-125">Olá estado de segurança de serviços do Azure que armazenam ou transmitir dados pessoais é avaliado tooidentify oportunidades toobetter proteger dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="aaf5b-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="aaf5b-126">Diretrizes de proteção de dados</span><span class="sxs-lookup"><span data-stu-id="aaf5b-126">Data protection guidance</span></span>

<span data-ttu-id="aaf5b-127">Olá artigos a seguir contêm técnica tooguidance como que ajudarão você a atingir os objetivos de proteção de dados pessoais Olá listados acima:</span><span class="sxs-lookup"><span data-stu-id="aaf5b-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="aaf5b-128">Tecnologias de criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="aaf5b-129">Tecnologias de criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="aaf5b-130">Tecnologias de acesso e identidade do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="aaf5b-131">Tecnologias de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="aaf5b-132">Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="aaf5b-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aaf5b-133">Next steps</span></span>

- [<span data-ttu-id="aaf5b-134">Site de Informações de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="aaf5b-135">Central de Confiabilidade da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aaf5b-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="aaf5b-136">Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="aaf5b-137">Blog da equipe de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="aaf5b-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="aaf5b-138">Blog do Azure.com – Segurança</span><span class="sxs-lookup"><span data-stu-id="aaf5b-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
