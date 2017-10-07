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
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C: gerenciamento de ameaças

O gerenciamento de ameaças inclui planejamento para proteção contra ataques ao sistema e às redes. Ataques de negação de serviço podem fazer com recursos de usuários toointended não está disponível. Tooresources de acesso toounauthorized do cliente potencial de ataques de senha. O Azure Active Directory B2C (Azure AD B2C) tem recursos internos que podem ajudá-lo a proteger seus dados contra essas ameaças de várias maneiras.

## <a name="denial-of-service-attacks"></a>Ataques de negação de serviço

B2C do Azure AD usa técnicas de detecção e atenuação como SYN cookies e tooprotect limites de taxa e conexão subjacente recursos contra ataques de negação de serviço.

## <a name="password-attacks"></a>Ataques de senha

O Azure AD B2C também tem técnicas de mitigação prontas para ataques de senha. A mitigação inclui ataques de senhas de força bruta e ataques de senhas de dicionário. Senhas que são definidas pelos usuários são necessária toobe razoavelmente complexo. Usando vários sinais, Azure AD B2C analisa integridade Olá de solicitações. B2C do Azure AD é projetado toointelligently diferenciar usuários pretendidos de hackers e botnets. B2C do AD do Azure fornece uma estratégia sofisticados toolock contas baseadas em senhas Olá inseridas na probabilidade de saudação de um ataque.

Para obter mais informações, visite Olá [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).
