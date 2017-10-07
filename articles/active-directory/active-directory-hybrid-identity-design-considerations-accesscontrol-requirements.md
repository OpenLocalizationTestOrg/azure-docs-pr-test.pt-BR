---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de controle de acesso | Microsoft Docs"
description: "Abrange Olá colunas de identidade e identificação de requisitos de acesso para recursos para usuários em um ambiente híbrido."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Determina os requisitos de controle de acesso para sua solução de identidade híbrida
Durante a criação de uma organização sua solução de identidade híbrida eles também podem usar esta oportunidade tooreview acessar requisitos para recursos de saudação que estão planejando toomake disponível para os usuários. acesso a dados Olá cruzada todas as quatro colunas de identidade, que são:

* Administração
* Autenticação
* Autorização
* Auditoria

seções de saudação que segue abordará autenticação e autorização em mais detalhes, administração e a auditoria são parte do ciclo de vida de identidade híbrida hello. Leia [Determinar as tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) para saber mais sobre esses recursos.

> [!NOTE]
> Leitura [Olá quatro colunas de identidade - gerenciamento de identidade no hello idade de TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) para obter mais informações sobre cada um dessas colunas.
> 
> 

## <a name="authentication-and-authorization"></a>Autenticação e autorização
Há cenários diferentes para autenticação e autorização, esses cenários terá requisitos específicos que devem ser atendidos pela solução de identidade híbrida Olá empresa Olá é tooadopt contínuo. Cenários que envolvem tooBusiness Business (B2B) comunicação pode adicionar um desafio extra para administradores de TI desde que eles precisarão tooensure que método de autenticação e autorização de hello usado pela organização Olá pode se comunicar com seus parceiros comerciais. Durante a saudação criar processo para obter os requisitos de autenticação e autorização, certifique-se de que Olá perguntas a seguir são atendidos:

* Sua organização irá autenticar e autorizar somente os usuários localizados em seu sistema de gerenciamento de identidade?
  * Há planos para cenários B2B?
  * Se Sim, você já sabe quais protocolos (SAML, OAuth, Kerberos, Tokens ou certificados) serão ser usado tooconnect ambas as empresas?
* Solução de identidade híbrida Olá vai tooadopt dá suporte a esses protocolos?

Outro tooconsider ponto importante é onde o repositório de autenticação de saudação que será usado por parceiros e usuários estarão localizado e toobe de modelo administrativo Olá usado. Considere Olá duas opções principais a seguir:

* Centralizado: em Olá esse modelo credenciais do usuário, políticas e administração podem ser centralizado local ou na nuvem hello.
* Híbrido: em Olá esse modelo credenciais do usuário, políticas e administração será centralizado local e um replicadas na nuvem hello.

Qual modelo de sua organização adotarão irá variar de acordo requisitos de negócios tootheir, você deseja tooanswer Olá tooidentify perguntas em que o sistema de gerenciamento de identidade Olá residirá e Olá toouse do modo de administrador a seguir:

* Sua organização tem atualmente um gerenciamento de identidade local?
  * Em caso afirmativo, eles planejam tookeep-lo?
  * Há algum requisito de conformidade ou regulamentação que sua organização deve seguir que impõe qual sistema de gerenciamento de identidade Olá deve residir?
* Sua organização usar o logon único para aplicativos localizados no local ou na nuvem Olá?
  * Em caso afirmativo, a adoção de saudação de um modelo de identidade híbrida afeta esse processo?

## <a name="access-control"></a>Controle de Acesso
Enquanto a autenticação e autorização são os principais elementos tooenable acessar toocorporate dados por meio da validação do usuário, também é importante toocontrol nível de saudação de acesso que esses usuários terão e nível de saudação de administradores de acesso terá sobre Olá recursos que estão gerenciando. Sua solução de identidade híbrida deve ser capaz de tooprovide acesso granular tooresources, controle de acesso de base de função e delegação. Certifique-se de que Olá pergunta a seguir são respondidas sobre controle de acesso:

* Sua empresa tem mais de um usuário com privilégios elevados toomanage seu sistema de identidade?
  * Se Sim, cada usuário precisar Olá nível mesmo de acesso?
* Seria necessário toodelegate acesso toousers toomanage específico recursos de sua empresa?
  * Em caso afirmativo, com que frequência isso acontece?
* Sua empresa precisaria toointegrate recursos de controle de acesso entre local e nuvem recursos?
* Sua empresa precisaria toolimit tooresources de acesso de acordo com as condições de toosome?
* Sua empresa teria qualquer aplicativo que precisa acessar toosome recursos de controle personalizado?
  * Em caso afirmativo, esses aplicativos localização (local ou na nuvem Olá)?
  * Em caso afirmativo, onde estão os recursos de destino localizados (local ou na nuvem Olá)?

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.  Depois de responder a essas perguntas, você selecionará a opção que melhor se ajusta às necessidades de sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Determinar requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

