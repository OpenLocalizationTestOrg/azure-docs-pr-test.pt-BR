---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de autenticação multifator"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Determinar os requisitos de autenticação multifator para sua solução de identidade híbrida
Em um mundo de mobilidade com usuários que acessam dados e aplicativos em nuvem hello e de qualquer dispositivo, proteger essas informações se torna muito importante.  Todos os dias há um novo título sobre violação de segurança.  Embora, não há nenhuma garantia contra falhas desse tipo, a autenticação multifator, fornece uma camada adicional de segurança toohelp evitar essas violações.
Iniciar avaliação de requisitos de organizações Olá para autenticação multifator. Ou seja, o que é Olá organização tentar toosecure.  Essa avaliação é requisitos técnicos do hello toodefine importantes para configurar e habilitar os usuários de organizações Olá para autenticação multifator.

> [!NOTE]
> Se você não estiver familiarizado com o MFA e o que ele faz, ela é altamente recomendável que você leia o artigo Olá [o que é o Azure multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue anterior ler esta seção.
> 
> 

Verifique a seguir Olá tooanswer-se de que:

* Sua empresa está tentando toosecure aplicativos da Microsoft? 
* Como esses aplicativos são publicados?
* Sua empresa oferece acesso remoto tooallow funcionários tooaccess local aplicativos?

Em caso afirmativo, que tipo de acesso remoto? Você também precisa tooevaluate onde os usuários de saudação que acessam esses aplicativos serão localizados. Essa avaliação é outra estratégia de autenticação multifator adequada etapa importante toodefine hello. Certifique-se de saudação tooanswer perguntas a seguir:

* Onde estão localizados os usuários Olá vai toobe?
* Podem ser localizados em qualquer lugar?
* Sua empresa deseja tooestablish restrições de acordo com o local do usuário toohello?

Depois de compreender esses requisitos, é importante tooalso avaliar Olá requisitos de usuário para autenticação multifator. Essa avaliação é importante porque ele definirá requisitos Olá para implementar a autenticação multifator. Certifique-se de saudação tooanswer perguntas a seguir:

* Os usuários de saudação estão familiarizados com autenticação multifator?
* Alguns usos será uma autenticação adicional tooprovide necessário?  
  * Se Sim, todos os Olá tempo, quando provenientes de redes externas, ou ao acessar aplicativos específicos, ou em outras condições?
* Os usuários de saudação precisarão de treinamento sobre como toosetup e implementar a autenticação multifator?
* Quais são os principais cenários de saudação que sua empresa deseja tooenable multi-factor authentication para seus usuários?

Depois de responder a perguntas anteriores de hello, será toounderstand capaz de se não houver autenticação multifator já foi implementado no local. Essa avaliação é requisitos técnicos do hello toodefine importantes para configurar e habilitar os usuários de organizações Olá para autenticação multifator. Certifique-se de saudação tooanswer perguntas a seguir:

* Sua empresa precisa de contas com privilégios de tooprotect com MFA?
* Sua empresa precisa tooenable MFA para determinados aplicativos por motivos de conformidade?
* Sua empresa precisa tooenable MFA para todos os usuários qualificados desses aplicativos ou somente administradores?
* Você precisa tem MFA sempre habilitada ou somente quando os usuários de saudação estiverem conectados à sua rede corporativa?

## <a name="next-steps"></a>Próximas etapas
[Definir uma estratégia de adoção de identidade híbrida](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Confira também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

