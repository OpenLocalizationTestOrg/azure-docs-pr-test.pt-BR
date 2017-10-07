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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="0dd75-103">Azure Active Directory B2C: gerenciamento de ameaças</span><span class="sxs-lookup"><span data-stu-id="0dd75-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="0dd75-104">O gerenciamento de ameaças inclui planejamento para proteção contra ataques ao sistema e às redes.</span><span class="sxs-lookup"><span data-stu-id="0dd75-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="0dd75-105">Ataques de negação de serviço podem fazer com recursos de usuários toointended não está disponível.</span><span class="sxs-lookup"><span data-stu-id="0dd75-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="0dd75-106">Tooresources de acesso toounauthorized do cliente potencial de ataques de senha.</span><span class="sxs-lookup"><span data-stu-id="0dd75-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="0dd75-107">O Azure Active Directory B2C (Azure AD B2C) tem recursos internos que podem ajudá-lo a proteger seus dados contra essas ameaças de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="0dd75-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="0dd75-108">Ataques de negação de serviço</span><span class="sxs-lookup"><span data-stu-id="0dd75-108">Denial-of-service attacks</span></span>

<span data-ttu-id="0dd75-109">B2C do Azure AD usa técnicas de detecção e atenuação como SYN cookies e tooprotect limites de taxa e conexão subjacente recursos contra ataques de negação de serviço.</span><span class="sxs-lookup"><span data-stu-id="0dd75-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="0dd75-110">Ataques de senha</span><span class="sxs-lookup"><span data-stu-id="0dd75-110">Password attacks</span></span>

<span data-ttu-id="0dd75-111">O Azure AD B2C também tem técnicas de mitigação prontas para ataques de senha.</span><span class="sxs-lookup"><span data-stu-id="0dd75-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="0dd75-112">A mitigação inclui ataques de senhas de força bruta e ataques de senhas de dicionário.</span><span class="sxs-lookup"><span data-stu-id="0dd75-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="0dd75-113">Senhas que são definidas pelos usuários são necessária toobe razoavelmente complexo.</span><span class="sxs-lookup"><span data-stu-id="0dd75-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="0dd75-114">Usando vários sinais, Azure AD B2C analisa integridade Olá de solicitações.</span><span class="sxs-lookup"><span data-stu-id="0dd75-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="0dd75-115">B2C do Azure AD é projetado toointelligently diferenciar usuários pretendidos de hackers e botnets.</span><span class="sxs-lookup"><span data-stu-id="0dd75-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="0dd75-116">B2C do AD do Azure fornece uma estratégia sofisticados toolock contas baseadas em senhas Olá inseridas na probabilidade de saudação de um ataque.</span><span class="sxs-lookup"><span data-stu-id="0dd75-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="0dd75-117">Para obter mais informações, visite Olá [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="0dd75-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
