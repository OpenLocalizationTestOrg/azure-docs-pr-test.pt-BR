---
title: aaaAzure multi-Factor Authentication - como ele funciona
description: "Autenticação multifator do Azure ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a>Como funciona o Azure Multi-Factor Authentication
segurança de saudação de verificação em duas etapas é sua abordagem em camadas. O comprometimento de vários fatores de autenticação apresenta um desafio significativo para os invasores. Mesmo se um invasor toolearn Olá a senha de usuário, é inútil sem também ter posse do dispositivo confiável hello. 

![Prova](./media/multi-factor-authentication-how-it-works/howitworks.png)

Autenticação multifator do Azure ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple.  Ele fornece segurança adicional, exigindo uma segunda forma de autenticação e fornece autenticação forte por meio de uma variedade de opções de verificação fácil.


## <a name="methods-available-for-two-step-verification"></a>Métodos disponíveis para verificação em duas etapas
Quando um usuário entra, uma verificação adicional é enviada toohello usuário.  Olá seguem uma lista de métodos que podem ser usados para essa verificação de segundo.

| Método de verificação | Descrição |
| --- | --- |
| chamada telefônica |Uma chamada é feita de telefone registrado tooa do usuário. usuário Olá insere um PIN, se necessário, em seguida, pressiona a tecla # de saudação. |
| mensagem de texto |Uma mensagem de texto é enviada celular do usuário tooa com um código de seis dígitos. usuário Olá insere esse código na página de entrada hello. |
| Notificação de aplicativo móvel |Uma solicitação de verificação é enviada Smartphone do usuário tooa. Olá usuário digita um PIN, se necessário, em seguida, seleciona **verificar** no aplicativo móvel hello. |
| Código de verificação do aplicativo móvel |aplicativo móvel Hello, que está em execução no Smartphone do usuário, exibe um código de verificação que muda a cada 30 segundos. usuário Olá localiza o código mais recente hello e insere-o na página de entrada hello. |
| Tokens OATH de terceiros | Servidor de autenticação multifator do Azure pode ser configurado tooaccept métodos de verificação de terceiros. |

O Azure Multi-Factor Authentication fornece métodos de verificação selecionável para a nuvem e o servidor. É possível escolher quais métodos estarão disponíveis para os usuários: chamada telefônica, texto, notificação no aplicativo ou códigos do aplicativo. Para obter mais informações, consulte os [métodos de verificação selecionáveis](multi-factor-authentication-whats-next.md#selectable-verification-methods).

## <a name="next-steps"></a>Próximas etapas

- Leia sobre Olá diferente [versões e os métodos de consumo para autenticação multifator do Azure](multi-factor-authentication-versions-plans.md)

- Escolha se toodeploy Azure MFA [na nuvem de saudação ou no local](multi-factor-authentication-get-started.md)

- Leia as respostas para as [Perguntas frequentes](multi-factor-authentication-faq.md)