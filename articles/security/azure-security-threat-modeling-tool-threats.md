---
title: "aaaThreats - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "Página de categoria de ameaça de Olá, ferramenta de modelagem de ameaças do Microsoft, que contém as categorias para expostos gerado ameaças."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Ameaças da Microsoft Threat Modeling Tool

Olá, ferramenta de modelagem de ameaça é um elemento de núcleo do hello Microsoft Security Development Lifecycle (SDL). Ele permite que o software arquitetos tooidentify e atenuar problemas potenciais de segurança no início, quando eles são tooresolve relativamente fácil e econômica. Como resultado, ele reduz significativamente o custo total de desenvolvimento de saudação. Além disso, projetamos ferramenta Olá com especialistas de segurança não em mente, facilitando a modelagem de ameaças para todos os desenvolvedores, fornecendo uma orientação clara sobre como criar e analisar os modelos de risco.

> Visite Olá  **[ferramenta de modelagem de ameaça](./azure-security-threat-modeling-tool.md)**  tooget iniciado hoje mesmo!

Olá, ferramenta de modelagem de ameaças ajuda a responder algumas perguntas, como Olá mostrados abaixo:

* Como um invasor pode alterar os dados de autenticação Olá?
* Qual é o impacto de saudação se um invasor pode ler dados de perfil de usuário Olá?
* O que acontece se o acesso é negado toohello banco de dados de perfil de usuário?

## <a name="stride-model"></a>Modelo STRIDE

Ajuda de toobetter formular esses tipos de perguntas pontuais, Microsoft usa Olá STRIDE modelo que categoriza os diferentes tipos de ameaças e simplifica Olá conversas geral de segurança.

| Categoria | Descrição |
| -------- | ----------- |
| **Falsificação** | Envolve acessar ilegalmente e, em seguida, usando as informações de autenticação de outro usuário, como nome de usuário e senha |
| **Violação** | Envolve a modificação mal-intencionada Olá dos dados. Exemplos incluem alterações não autorizadas feitas toopersistent dados, como o que é mantido em um banco de dados e a alteração de saudação de dados conforme ela flui entre dois computadores em uma rede aberta, como saudação da Internet |
| **Repúdio** | Associado aos usuários que negam a execução de uma ação sem ter qualquer tooprove de modo contrário — por exemplo, um usuário executa uma operação ilegal em um sistema que não tem as operações do hello capacidade tootrace Olá proibido. Não-repúdio refere-se a capacidade de toohello de ameaças de recusa de toocounter um sistema. Por exemplo, um usuário que adquire um item pode ter toosign item Olá após o recebimento. fornecedor de saudação pode então usar Olá assinado recebimento como evidência de que o usuário Olá recebeu pacote hello |
| **Divulgação de Informações** | Envolve a exposição de saudação do tooindividuals informações que não deveriam toohave acesso tooit — por exemplo, capacidade de saudação do usuários tooread um arquivo que não estavam acesso concedido para ou hello capacidade de um invasor tooread os dados em trânsito entre dois computadores |
| **Negação de Serviço** | Usuários do serviço de toovalid de negar ataques negação de serviço (DoS) — por exemplo, pela criação de um servidor Web temporariamente indisponível ou inutilizável. Você deve se proteger contra certos tipos DoS ameaças simplesmente tooimprove disponibilidade e confiabilidade |
| **Elevação de Privilégio** | Um usuário sem privilégios obtém acesso privilegiado e, portanto, tem toocompromise de acesso suficientes ou destruir todo o sistema hello. Elevação de ameaças de privilégio incluem nas situações em que um invasor tem efetivamente penetração todos os recursos do sistema e se tornam parte do sistema Olá confiável em si, de fato uma situação perigosa |

## <a name="next-steps"></a>Próximas etapas

Continuar muito**[atenuações de ferramenta de modelagem de ameaças](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn Olá diferentes maneiras pode reduzir essas ameaças com o Azure.
