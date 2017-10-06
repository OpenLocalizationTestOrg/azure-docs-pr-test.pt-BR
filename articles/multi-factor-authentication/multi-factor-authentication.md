---
title: "aaaLearn sobre a verificação em duas etapas no Azure MFA | Microsoft Docs"
description: "O que é autenticação multifator do Azure, por que usar MFA, obter mais informações sobre o cliente de autenticação multifator hello e métodos diferentes de saudação e versões disponíveis. "
keywords: "Introdução tooMFA, visão geral de mfa, o que é o mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>O que é o Azure Multi-Factor Authentication?
Verificação em duas etapas é um método de autenticação que requer mais de um método de verificação e adiciona uma segunda camada crítica de segurança toouser entradas e transações. Ela funciona exigindo dois ou mais Olá métodos de verificação a seguir:

* Algo que você sabe (normalmente, uma senha)
* Algo que você tem (um dispositivo confiável que não pode ser facilmente clonado, como um telefone)
* Algo seu (biometria)

<center>![Nome de usuário e senha](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Cartão inteligente virtual](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome de usuário e senha](./media/multi-factor-authentication/cert.png)</center>

O Azure MFA é uma solução de verificação em duas etapas da Microsoft. Azure MFA ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de métodos de verificação, incluindo chamada telefônica, mensagem de texto ou verificação de aplicativo móvel.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Por que usar o Azure Multi-Factor Authentication?
Hoje, mais do que nunca, as pessoas estão cada vez mais conectadas. Com os Smartphones, tablets, laptops e computadores, as pessoas têm várias opções diferentes como eles serão tooconnect e permanecem conectados a qualquer momento. As pessoas podem acessar suas contas e aplicativos de qualquer lugar, o que significa que elas podem concluir mais tarefas de trabalho e atender melhor os seus clientes.

Autenticação multifator do Azure é um toouse fácil, escalonável e solução confiável que fornece um segundo método de autenticação para que os usuários sempre sejam protegidos.

| ![TooUse fácil](./media/multi-factor-authentication/simple.png) | ![Escalonável](./media/multi-factor-authentication/scalable.png) | ![Sempre protegidos](./media/multi-factor-authentication/protected.png) | ![Confiável](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Toouse fácil** |**Escalonável** |**Sempre protegidos** |**Confiável** |

* **Fácil tooUse** -Azure multi-Factor Authentication é simple tooset backup e uso. Olá proteção extra que vem com o Azure multi-Factor Authentication permite que os usuários toomanage seus próprios dispositivos. O melhor de tudo, em muitos casos ela pode ser configurada com apenas alguns cliques.
* **Escalonável** -autenticação multifator do Azure usa a energia Olá da nuvem de saudação e integra-se ao seu local AD e aplicativos personalizados. Essa proteção é estendida até mesmo tooyour cenários de alto volume de missão crítica.
* **Sempre protegido** -autenticação multifator do Azure fornece autenticação forte usando padrões da indústria mais altos hello.
* **Confiável** - Garantimos 99,9% de disponibilidade do Azure Multi-Factor Authentication. Olá serviço é considerado indisponível quando não é possível tooreceive ou processo solicitações de verificação para verificação do hello em duas etapas.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [Como funciona a Autenticação Multifator do Azure](multi-factor-authentication-how-it-works.md)

- Leia sobre Olá diferente [versões e os métodos de consumo para autenticação multifator do Azure](multi-factor-authentication-versions-plans.md)
