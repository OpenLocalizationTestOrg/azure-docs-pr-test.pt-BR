---
title: Proteger dados pessoais no Microsoft Azure | Microsoft Docs
description: "Primeiro artigo de uma série de artigos para ajudá-lo a usar o Azure para proteger dados pessoais"
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
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="9b3f5-103">Proteger dados pessoais no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="9b3f5-104">Este artigo apresenta uma série de artigos que ajuda a usar as tecnologias e os serviços de segurança do Azure para proteger dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-104">This article introduces a series of articles that help you use Azure security technologies and services to protect personal data.</span></span> <span data-ttu-id="9b3f5-105">Este é um requisito fundamental para muitas iniciativas de governança e conformidade corporativas e do setor.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="9b3f5-106">O cenário, a declaração do problema e as metas da empresa são incluídos aqui.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-106">The scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="9b3f5-107">Cenário e declaração do problema</span><span class="sxs-lookup"><span data-stu-id="9b3f5-107">Scenario and problem statement</span></span>

<span data-ttu-id="9b3f5-108">Uma empresa de cruzeiro de grande porte, com sede nos Estados Unidos, está expandindo suas operações para oferecer roteiros nos mares Mediterrâneo, Adriático e Báltico, bem como nas Ilhas Britânicas.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="9b3f5-109">Para dar suporte a esses esforços, ela adquiriu várias linhas de cruzeiro menores localizadas na Itália, na Alemanha, na Dinamarca e no Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="9b3f5-110">A empresa usa o Microsoft Azure para armazenar dados corporativos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="9b3f5-111">Isso pode incluir funcionário e/ou informações do cliente, como:</span><span class="sxs-lookup"><span data-stu-id="9b3f5-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="9b3f5-112">endereços</span><span class="sxs-lookup"><span data-stu-id="9b3f5-112">addresses</span></span>
- <span data-ttu-id="9b3f5-113">números de telefone</span><span class="sxs-lookup"><span data-stu-id="9b3f5-113">phone numbers</span></span>
- <span data-ttu-id="9b3f5-114">números de identificação fiscal</span><span class="sxs-lookup"><span data-stu-id="9b3f5-114">tax identification numbers</span></span>
- <span data-ttu-id="9b3f5-115">informações de médicas</span><span class="sxs-lookup"><span data-stu-id="9b3f5-115">medical information</span></span>
- <span data-ttu-id="9b3f5-116">informações de cartão de crédito</span><span class="sxs-lookup"><span data-stu-id="9b3f5-116">credit card information</span></span>

<span data-ttu-id="9b3f5-117">A empresa deve proteger a privacidade dos dados de funcionário e o cliente ao fazer dados acessíveis para os departamentos que precisam dela.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="9b3f5-118">(como departamentos de folha de pagamento e reservas)</span><span class="sxs-lookup"><span data-stu-id="9b3f5-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="9b3f5-119">Metas da empresa</span><span class="sxs-lookup"><span data-stu-id="9b3f5-119">Company goals</span></span> 

- <span data-ttu-id="9b3f5-120">As fontes de dados que contêm dados pessoais são criptografadas quando residem no armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="9b3f5-121">Os dados pessoais transferidos de um local para outro são criptografados enquanto estão em trânsito.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-121">Personal data that is transferred from one location to another is encrypted while in-transit.</span></span> <span data-ttu-id="9b3f5-122">Isso será verdadeiro se os dados estiverem viajando pela rede virtual ou na Internet entre os data centers corporativos e a nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-122">This is true if the data is traveling across the virtual network or across the Internet between the corporate datacenter and the Azure cloud.</span></span>

- <span data-ttu-id="9b3f5-123">A confidencialidade e a integridade dos dados pessoais são protegidas contra o acesso não autorizado por tecnologias de controle de acesso e gerenciamento de identidade forte.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="9b3f5-124">Os dados pessoais são protegidos contra a exposição por meio da violação de dados com o monitoramento de ameaças e vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="9b3f5-125">O estado de segurança dos serviços do Azure que armazenam ou transmitem dados pessoais é avaliado para identificar oportunidades para proteger melhor os dados pessoais.</span><span class="sxs-lookup"><span data-stu-id="9b3f5-125">The security state of Azure services that store or transmit personal data is assessed to identify opportunities to better protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="9b3f5-126">Diretrizes de proteção de dados</span><span class="sxs-lookup"><span data-stu-id="9b3f5-126">Data protection guidance</span></span>

<span data-ttu-id="9b3f5-127">Os seguintes artigos contêm diretrizes de instruções técnicas que ajudarão você a atingir as metas de proteção de dados pessoais listadas acima:</span><span class="sxs-lookup"><span data-stu-id="9b3f5-127">The following articles contain technical how-to guidance that will help you attain the personal data protection goals listed above:</span></span>

- [<span data-ttu-id="9b3f5-128">Tecnologias de criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="9b3f5-129">Tecnologias de criptografia do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="9b3f5-130">Tecnologias de acesso e identidade do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="9b3f5-131">Tecnologias de segurança de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="9b3f5-132">Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="9b3f5-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b3f5-133">Next steps</span></span>

- [<span data-ttu-id="9b3f5-134">Site de Informações de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="9b3f5-135">Central de Confiabilidade da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b3f5-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="9b3f5-136">Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="9b3f5-137">Blog da equipe de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="9b3f5-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="9b3f5-138">Blog do Azure.com – Segurança</span><span class="sxs-lookup"><span data-stu-id="9b3f5-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
