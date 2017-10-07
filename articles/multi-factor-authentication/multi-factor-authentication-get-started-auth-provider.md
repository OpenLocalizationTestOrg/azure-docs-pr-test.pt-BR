---
title: "aaaGet iniciado o provedor de autenticação multifator do Azure | Microsoft Docs"
description: "Saiba como toocreate um provedor de autenticação multifator do Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Introdução a um Provedor de Autenticação Multifator do Azure
A autenticação em duas etapas está disponível por padrão para os administradores globais que têm o Azure Active Directory e os usuários do Office 365. No entanto, se desejar aproveitar tootake [recursos avançados](multi-factor-authentication-whats-next.md) , em seguida, você deve comprar uma versão completa da saudação do Azure multi-Factor Authentication (MFA).

Um provedor de autenticação multifator do Azure é usado tootake proveito dos recursos fornecidos pelo versão completa de saudação do Azure MFA. É para os usuários que **não têm licenças por meio do Azure MFA, Azure AD Premium ou Enterprise Mobility + Security (EMS)**.  MFA do Azure, Azure AD Premium e EMS incluem a versão completa de saudação do Azure MFA por padrão. Se você tiver licenças, não precisará de um Provedor de Autenticação Multifator do Azure.

Um provedor de Azure multi-Factor Auth é Olá toodownload necessário SDK.

> [!IMPORTANT]
> toodownload Olá SDK, você precisa toocreate um provedor de autenticação multifator do Azure, mesmo se você tiver licenças de Azure MFA, AAD Premium ou EMS.  Se você criar um provedor de autenticação multifator do Azure para essa finalidade e já tiver licenças, ser Olá se toocreate provedor com hello **por usuário habilitado** modelo. Em seguida, vincule toohello diretório Olá provedor contém Olá licenças de Azure MFA, o Azure AD Premium ou EMS. Essa configuração garante que você será cobrado somente se você tiver mais de usuários exclusivos executar verificação de duas etapas que número de saudação de licenças que você possui.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>O que é um Provedor de Autenticação Multifator do Azure?

Se você não tiver licenças para o Azure multi-Factor Authentication, você pode criar uma verificação em duas etapas de toorequire de provedor de autenticação para os usuários. Se você estiver desenvolvendo um aplicativo personalizado e desejar tooenable MFA do Azure, crie um provedor de autenticação e [baixar Olá SDK](multi-factor-authentication-sdk.md).

Há dois tipos de provedores de autenticação e distinção de saudação é em torno de como a sua assinatura do Azure é cobrada. opção de por autenticação Olá calcula o número de Olá de autenticações executadas em seu locatário em um mês. Essa será a melhor opção se você tiver um número de usuários que se autenticam apenas ocasionalmente, como se você exigir MFA para um aplicativo personalizado. opção de por usuário Olá calcula o número de saudação de outras pessoas em seu locatário que execute a verificação em duas etapas em um mês. Essa é a melhor opção se você tiver alguns usuários com licenças, mas precisa de usuários do tooextend MFA toomore além dos limites de licença.

## <a name="create-a-multi-factor-auth-provider"></a>Criar um Provedor de Autenticação Multifator
Use Olá seguindo as etapas toocreate um provedor de autenticação multifator do Azure. Provedores de autenticação multifator do Azure só podem ser criados em Olá portal clássico do Azure. Se você não pode entrar toohello portal clássico do Azure, verifique toomake-se de que seu locatário do AD do Azure [associado a uma assinatura do Azure](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.
2. Olá esquerda, selecione **do Active Directory**.
3. Na página do Active Directory hello, na parte superior do hello, selecione **provedores de autenticação multifator**.
   
   ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Na parte inferior da saudação, clique em **novo**.
   
   ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. Em Serviços de Aplicativos, selecione **Provedor de Autenticação Multifator**
   
   ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Selecione **Criação Rápida**.
   
   ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Preencha os campos a seguir de saudação e selecione **criar**.
   1. **Nome** – hello nome da saudação provedor de autenticação multifator.
   2. **Modelo de Uso** – Escolha uma das duas opções:
      * Por Autenticação: modelo de compra que cobra por autenticação. Normalmente usado para cenários que usam o Autenticação Multifator do Azure em um aplicativo voltado para o consumidor.
      * Por Usuário Habilitado: o modelo de compra que cobra por usuário habilitado. Normalmente usado para tooapplications de acesso de funcionário como o Office 365. Escolha esta opção se você tiver alguns usuários que já estão licenciados para o MFA do Azure.
   3. **Diretório** – Olá Active Directory do Azure locatário que Olá provedor do multi-Factor Authentication está associado. Esteja ciente do seguinte hello:
      * Não é necessário um toocreate de diretório do AD do Azure um provedor de autenticação multifator. Deixe essa caixa em branco se você estiver planejando somente Olá toodownload servidor Azure multi-Factor Authentication ou o SDK.
      * Olá provedor do multi-Factor Authentication deve ser associado uma vantagem de tootake de diretório do AD do Azure de Olá recursos avançados.
      * Somente um Provedor de Autenticação Multifator pode ser associado a um diretório do Azure AD.  
      ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Depois de clicar em criar, hello provedor de autenticação multifator é criado e você verá uma mensagem dizendo: **criado com êxito o provedor de autenticação multifator**. Clique em **OK**.  
   
   ![Criação de um provedor MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Gerenciar um Provedor de Autenticação Multifator

Você não pode alterar o uso de saudação após a criação de um provedor de MFA de modelo (por usuário habilitado ou por autenticação). No entanto, você pode excluir o provedor MFA de saudação e, em seguida, criar uma com um modelo de uso diferentes.

Se hello a atual provedor de autenticação multifator está associado um diretório do AD do Azure (também conhecido como um locatário Azure AD), com segurança poderá excluir o provedor MFA de saudação e criar um locatário toohello vinculado mesmo Azure AD. Como alternativa, se você adquiriu suficiente MFA, o Azure AD Premium, ou o Enterprise Mobility + a segurança (EMS) licenças toocover todos os usuários que estão habilitados para MFA, você pode excluir provedor MFA de saudação completamente.

Se seu provedor MFA não estiver vinculado tooan AD do Azure locatário ou vincular Olá novo MFA provedor tooa diferente do AD do Azure locatário, as configurações de usuário e opções de configuração não são transferidas. Além disso, servidores do Azure MFA existentes necessário toobe reativado usando credenciais de ativação gerados por meio de Olá novo provedor de MFA. Reativando Olá servidores MFA toolink-los toohello novo provedor de MFA não afeta a chamada telefônica e autenticação de mensagem de texto, mas o aplicativo móvel notificações irá parar de funcionar para todos os usuários até que eles reativarem o aplicativo móvel hello.

## <a name="next-steps"></a>Próximas etapas

[Baixar Olá SDK multi-Factor Authentication](multi-factor-authentication-sdk.md)

[Definir as configurações da Autenticação Multifator](multi-factor-authentication-whats-next.md)
