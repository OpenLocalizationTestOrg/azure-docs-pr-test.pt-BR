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
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Determinar os requisitos de gerenciamento de conteúdo para sua solução de identidade híbrida
Noções básicas sobre requisitos de gerenciamento de conteúdo de saudação para seu negócio pode direcionar afetam sua decisão sobre qual toouse de solução de identidade híbrida. Com hello proliferação de vários dispositivos e a capacidade de saudação do usuários toobring seus próprios dispositivos ([BYOD](http://aka.ms/byodcg)), empresa Olá deve proteger seus próprios dados, mas ele também deve manter privacidade do usuário intacta. Normalmente quando um usuário tem seu próprio dispositivo ele pode ter também várias credenciais que serão alternar o acordo aplicativo toohello que ele usa. É importante toodifferentiate o conteúdo que foi criado usando credenciais pessoais versus Olá aqueles criados usando credenciais corporativas. Sua solução de identidade deverá ser capaz de toointeract com tooprovide de serviços de nuvem uma experiência perfeita toohello final ao garantir sua privacidade e aumentar a proteção de saudação contra vazamento de dados. 

Sua solução de identidade será aproveitada por diferentes controles técnicos em gerenciamento de conteúdo do pedido tooprovide conforme mostrado na figura a saudação abaixo:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Controles de segurança que aproveitarão o sistema de gerenciamento de identidade**

Em geral, os requisitos de gerenciamento de conteúdo utilizará seu sistema de gerenciamento de identidade no hello áreas a seguir:

* Privacidade: identificação usuário Olá que possui um recurso e aplicar a integridade de toomaintain Olá controles apropriados.
* Classificação de dados: identificar o usuário hello ou o grupo e o nível de objeto tooan de acesso de acordo com a classificação de tooits. 
* Proteção contra vazamento de dados: controles de segurança responsáveis por proteger vazamento de tooavoid dados precisará toointeract com identidade Olá identidade toovalidate saudação do usuário. Isso também é importante para a finalidade de trilha de auditoria.

> [!NOTE]
> Leitura [classificação de dados para preparação de nuvem](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obter mais informações sobre as práticas recomendadas e diretrizes para a classificação de dados.
> 
> 

Ao planejar sua solução de identidade híbrida Certifique-se de que Olá a seguir são responder perguntas de acordo com os requisitos da organização tooyour:

* Sua empresa tem controles de segurança em vigor tooenforce privacidade dos dados?
  * Em caso afirmativo, esses controles de segurança será capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?
* Sua empresa usa a classificação de dados?
  * Em caso afirmativo, é Olá atual solução capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?
* Sua empresa atualmente tem qualquer solução de vazamento de dados? 
  * Em caso afirmativo, é Olá atual solução capaz de toointegrate com solução de identidade híbrida Olá que você está indo tooadopt?
* Sua empresa precisa tooaudit acesso tooresources?
  * Em caso afirmativo, que tipo de recursos?
  * Em caso afirmativo, qual nível de informação é necessário?
  * Em caso afirmativo, onde o log de auditoria Olá deve residir? Local ou na nuvem Olá?
* Sua empresa precisa tooencrypt qualquer e-mails que contenham dados confidenciais (CPFs, números de cartão de crédito, etc)?
* Sua empresa precisa tooencrypt todos os documentos/conteúdo compartilhado com parceiros de negócios externos?
* Sua empresa precisa de políticas corporativas de tooenforce em determinados tipos de emails (não responder a todos, não encaminhar)?

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.  Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Determinar requisitos de controle de acesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

