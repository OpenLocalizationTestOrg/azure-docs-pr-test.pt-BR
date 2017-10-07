---
title: "Azure Active Directory B2C: autenticação multifator | Microsoft Docs"
description: Como tooenable multi-Factor Authentication em aplicativos voltados para o consumidor protegida pelo Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: habilitar a Multi-Factor Authentication nos seus aplicativos voltados para o consumidor
B2C do Azure Active Directory (AD do Azure) integra-se diretamente ao [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) para que você pode adicionar uma segunda camada de experiências de segurança toosign-up e entrar em seus aplicativos voltados para o consumidor. E você pode fazer isso sem escrever uma única linha de código. No momentos damos suporte à verificação por ligação telefônica e mensagem de texto. Se você já tiver criado as políticas de credenciais e de entrada, ainda poderá habilitar a Multi-Factor Authentication.

> [!NOTE]
> A Multi-Factor Authentication também pode ser habilitada durante a criação de políticas de credenciais e de entrada, não apenas na edição de políticas existentes.
> 
> 

Esse recurso ajuda os aplicativos a lidar com cenários como a seguir hello:

* Você não precise de um aplicativo de tooaccess multi-Factor Authentication, mas você precisa tooaccess outro. Por exemplo, pode entrar em um aplicativo de seguro automaticamente com uma conta local ou social consumidor hello, mas deve verificar o número de telefone de saudação antes de acessar aplicativo inicial de seguro hello registrado no hello mesmo diretório.
* Você não exige autenticação multifator tooaccess um aplicativo em geral, mas você precisa tooaccess partes confidenciais do hello dentro dele. Por exemplo, consumidor Olá pode entrar tooa aplicativo com uma conta local ou social e verifique o saldo da conta de serviços bancários, mas deve verificar o número de telefone de saudação antes de tentar a transferência eletrônica.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Modificar tooenable sua política de inscrição multi-Factor Authentication
1. [Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Clique em **Políticas de inscrição**.
3. Clique em sua política de inscrição (por exemplo, "B2C_1_SiUp") tooopen-lo.
4. Clique em **autenticação multifator** e ativar Olá **estado** muito**ON**. Clique em **OK**.
5. Clique em **salvar** na parte superior de saudação da folha de saudação.

Você pode usar o recurso de "Executar agora" hello na experiência do consumidor Olá política tooverify hello. Confirme a seguir hello:

Uma conta de consumidor é criada no diretório antes de etapa de autenticação multifator Olá ocorre. Durante a etapa de saudação consumidor Olá é solicitado tooprovide seu número de telefone e verificar se ela. Se a verificação for bem-sucedida, o número de telefone hello está anexado toohello conta de consumidor para uso posterior. Mesmo se o consumidor Olá cancela ou descartada, ele podem ser feita tooverify um número de telefone novamente durante Olá próxima vez que entrar (com autenticação multifator habilitada).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Modificar sua política tooenable multi-Factor Authentication
1. [Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Clique em **Políticas de entrada**.
3. Clique em sua política de entrada (por exemplo, "B2C_1_SiIn") tooopen-lo. Clique em **editar** na parte superior de saudação da folha de saudação.
4. Clique em **autenticação multifator** e ativar Olá **estado** muito**ON**. Clique em **OK**.
5. Clique em **salvar** na parte superior de saudação da folha de saudação.

Você pode usar o recurso de "Executar agora" hello na experiência do consumidor Olá política tooverify hello. Confirme a seguir hello:

Quando o consumidor Olá entra (usando uma conta local ou social), se estiver conectado a um número de telefone verificado toohello conta de consumidor, ele ou ela é solicitada tooverify-lo. Se nenhum número de telefone estiver conectado, o consumidor Olá é solicitado tooprovide um e verificar se ela. Verificação bem-sucedida, o número de telefone Olá está anexado toohello conta de consumidor para uso posterior.

## <a name="multi-factor-authentication-on-other-policies"></a>Multi-Factor Authentication em outras políticas
Conforme descrito para políticas de inscrição & entrar acima, também é possível tooenable autenticação multifator inscrição ou políticas de senha e entrar redefinir as políticas. Ela estará disponível em breve nas políticas de edição de perfil.

