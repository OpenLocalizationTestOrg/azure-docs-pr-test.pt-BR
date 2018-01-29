---
title: "Saiba mais sobre a verificação em duas etapas no Azure MFA | Microsoft Docs"
description: "O que é a Autenticação Multifator do Azure (MFA, Multi-factor Authentication), por que usar MFA, mais informações sobre o cliente MFA e os diferentes métodos e versões disponíveis. "
keywords: "introdução ao MFA, visão do geral do mfa, o que é mfa"
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: joflore
ms.openlocfilehash: 63b717fb08861b0efe902400a8765f9515ed5b1a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>O que é a Autenticação Multifator do Azure?
A verificação em duas etapas é um método de autenticação que exige mais de um método de verificação e adiciona uma segunda camada crítica de segurança aos logons e às transações dos usuários. Ela funciona, exigindo dois ou mais dos métodos de verificação a seguir:

* Algo que você sabe (normalmente, uma senha)
* Algo que você tem (um dispositivo confiável que não pode ser facilmente clonado, como um telefone)
* Algo seu (biometria)

<center>![Nome de usuário e senha](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente virtual](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome de usuário e senha](./media/multi-factor-authentication/cert.png)</center>

A Autenticação Multifator do Azure é uma solução de verificação em duas etapas da Microsoft. O Azure MFA ajuda a proteger o acesso a dados e aplicativos, ao mesmo tempo que atende à demanda dos usuários por um processo de entrada simples. Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.

## <a name="why-use-azure-multi-factor-authentication"></a>Por que usar a Autenticação Multifator do Azure?
Hoje, mais do que nunca, as pessoas estão cada vez mais conectadas. Com smart phones, tablets, computadores portáteis e de secretária, as pessoas têm várias opções para acessar suas contas e aplicativos de todo o lado e permanecer conectados a qualquer momento.

A Autenticação Multifator do Azure é uma solução fácil de usar, escalonável e confiável que fornece um segundo método de autenticação para proteger os seus usuários.

| ![Fácil de usar](./media/multi-factor-authentication/simple.png) | ![Escalonável](./media/multi-factor-authentication/scalable.png) | ![Sempre protegidos](./media/multi-factor-authentication/protected.png) | ![Confiável](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Fácil de usar** |**Escalonável** |**Sempre protegidos** |**Confiável** |

* **Fácil de usar** – a Autenticação Multifator do Azure é simples de configurar e usar. A proteção extra que acompanha a Autenticação Multifator do Azure permite que os usuários gerenciem seus próprios dispositivos. O melhor de tudo, em muitos casos ela pode ser configurada com apenas alguns cliques.
* **Escalonável** – a Autenticação Multifator do Azure utiliza os recursos da nuvem e integra-se ao seu AD e a aplicativos personalizados locais. Essa proteção ainda é estendida aos seus cenários essenciais de missão de alto volume.
* **Sempre protegidos** - a Autenticação Multifator do Azure fornece autenticação forte usando os mais altos padrões do setor.
* **Confiável** - a Microsoft garante 99,9% de disponibilidade da Autenticação Multifator do Azure. O serviço é considerado indisponível quando não é possível receber ou processar solicitações de verificação para verificação em duas etapas.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [Como funciona a Autenticação Multifator do Azure](multi-factor-authentication-how-it-works.md)

- Leia sobre os diferentes [métodos de consumo e versões para a Autenticação Multifator do Azure](multi-factor-authentication-versions-plans.md)
