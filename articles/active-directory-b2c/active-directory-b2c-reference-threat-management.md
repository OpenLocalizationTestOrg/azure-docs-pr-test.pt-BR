---
title: "Azure Active Directory B2C: gerenciamento de ameaças| Microsoft Docs"
description: "Saiba mais sobre técnicas de detecção e mitigação de ataques de negação de serviço e ataques de senha no Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="91c3d-103">Azure Active Directory B2C: gerenciamento de ameaças</span><span class="sxs-lookup"><span data-stu-id="91c3d-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="91c3d-104">O gerenciamento de ameaças inclui planejamento para proteção contra ataques ao sistema e às redes.</span><span class="sxs-lookup"><span data-stu-id="91c3d-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="91c3d-105">Os ataques de negação de serviço podem tornar os recursos não disponíveis para usuários pretendidos.</span><span class="sxs-lookup"><span data-stu-id="91c3d-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="91c3d-106">Os ataques de senha ocasionam o acesso não autorizado aos recursos.</span><span class="sxs-lookup"><span data-stu-id="91c3d-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="91c3d-107">O Azure Active Directory B2C (Azure AD B2C) tem recursos internos que podem ajudá-lo a proteger seus dados contra essas ameaças de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="91c3d-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="91c3d-108">Ataques de negação de serviço</span><span class="sxs-lookup"><span data-stu-id="91c3d-108">Denial-of-service attacks</span></span>

<span data-ttu-id="91c3d-109">O Azure AD B2C usa técnicas de detecção e de mitigação como cookies SYN e limites de taxa e de conexão para proteger os recursos subjacentes contra esses ataques de negação de serviço.</span><span class="sxs-lookup"><span data-stu-id="91c3d-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="91c3d-110">Ataques de senha</span><span class="sxs-lookup"><span data-stu-id="91c3d-110">Password attacks</span></span>

<span data-ttu-id="91c3d-111">O Azure AD B2C também tem técnicas de mitigação prontas para ataques de senha.</span><span class="sxs-lookup"><span data-stu-id="91c3d-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="91c3d-112">A mitigação inclui ataques de senhas de força bruta e ataques de senhas de dicionário.</span><span class="sxs-lookup"><span data-stu-id="91c3d-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="91c3d-113">As senhas definidas pelos usuários devem ser de complexidade razoável.</span><span class="sxs-lookup"><span data-stu-id="91c3d-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="91c3d-114">Ao usar vários sinais, o Azure AD B2C analisa a integridade das solicitações.</span><span class="sxs-lookup"><span data-stu-id="91c3d-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="91c3d-115">O Azure AD B2C foi projetado para diferenciar, de forma inteligente, os usuários pretendidos de hackers e botnets.</span><span class="sxs-lookup"><span data-stu-id="91c3d-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="91c3d-116">O Azure AD B2C oferece uma estratégia sofisticada para bloquear contas com base nas senhas digitadas, na probabilidade de um ataque.</span><span class="sxs-lookup"><span data-stu-id="91c3d-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="91c3d-117">Para obter mais informações, consulte o [Centro de Confiabilidade da Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="91c3d-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
