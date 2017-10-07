---
title: "aaaHow tooget um locatário do AD do Azure | Microsoft Docs"
description: "Como tooget um Active Directory do Azure locatário para registrar e criação de aplicativos."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Como tooget um Active Directory do Azure locatário
No AD do Azure, um [locatário](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) é representativo de uma organização.  É uma instância dedicada do hello serviço do AD do Azure que uma organização recebe e detém quando se inscreve em um serviço de nuvem da Microsoft, como o Office 365, Microsoft Intune ou do Azure.  Cada locatário do AD do Azure é distinto e separado de outros diretórios do AD do Azure.  

Um locatário abriga usuários Olá em uma empresa e Olá informações sobre eles - suas senhas, dados de perfil de usuário, permissões e assim por diante.  Ele também contém grupos, aplicativos e outras informações referentes a organização tooan e sua segurança.

tooallow AD do Azure usuários toosign tooyour aplicativo, você deve registrar seu aplicativo em um locatário de sua preferência.  Publicar um aplicativo em um locatário do AD do Azure é **totalmente gratuito**.  Na verdade, a maioria dos desenvolvedores criará vários locatários e aplicativos para fins de experimentação, teste, desenvolvimento e preparo.  As organizações que se inscreve e consumam seu aplicativo podem optar toopurchase licenças se desejarem tootake proveito dos recursos avançados de diretório.

Então, como você faria para obter um locatário do AD do Azure?  Olá processo pode ser um pouco se diferentes você:

* [Tem uma assinatura existente do Office 365](#use-an-existing-office-365-subscription)
* [Tem uma assinatura existente do Azure associada a uma conta da Microsoft](#use-an-msa-azure-subscription)
* [Tem uma assinatura existente do Azure associada a uma conta organizacional](#use-an-organizational-azure-subscription)
* [Não ter nenhum Olá acima e toostart a partir do zero](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Usar uma assinatura existente do Office 365
Se houver uma assinatura do Office 365, você já terá um locatário do Azure AD! Você pode entrar no toohello [portal do Azure](https://portal.azure.com) com seu O365 conta e começar a usar o AD do Azure.

## <a name="use-an-msa-azure-subscription"></a>Usar uma assinatura do Azure MSA
Se você já se inscreveu anteriormente para uma assinatura do Azure com sua conta individual da Microsoft, você já tem um locatário!  Ao fazer logon em toohello [Portal do Azure](https://portal.azure.com), você será automaticamente registrado no locatário do tooyour padrão. Você está livre toouse este locatário que você consulte ajustar - mas talvez você queira toocreate uma conta de administrador organizacional.

toodo assim, siga estas etapas.  Como alternativa, você pode desejar toocreate um novo locatário e criar um administrador no locatário seguindo um processo semelhante.

1. Faça logon no hello [Portal do Azure](https://portal.azure.com) com sua conta individual
2. Navegue toohello seção de "Active Directory do Azure" do portal da saudação (encontrado na barra de navegação esquerdo hello, em **mais serviços**)
3. Você deve ser conectado automaticamente toohello "Diretório padrão", se não pode alternar pastas clicando no nome da sua conta no canto superior direito da saudação.
4. De saudação **tarefas rápidas** , escolha **adicionar um usuário**.
5. Em Olá Adicionar formulário de usuário, forneça Olá detalhes a seguir:

   * Nome: (escolha um valor apropriado)
   * Nome de usuário: (escolha um nome de usuário para esse administrador)
   * Perfil: (preencha os valores apropriados para o nome, sobrenome, cargo e departamento Olá)
   * Função: administrador global
6. Quando você tiver concluído Olá Adicionar formulário de usuário e recebe a senha temporária Olá para o novo usuário administrativo de saudação, ser toorecord-se de que essa senha, pois você precisará toologin com esse novo usuário na senha do pedido toochange hello. Você também pode enviar senha Olá diretamente toohello usuário usando um email alternativo.
7. Clique em **criar** novo usuário do toocreate hello.
8. senha temporária toochange hello, faça logon no [https://login.microsoftonline.com](https://login.microsoftonline.com) com esse novo usuário de conta e alterar a senha de saudação quando solicitado.

## <a name="use-an-organizational-azure-subscription"></a>Use uma assinatura organizacional do Azure
Se você já se inscreveu anteriormente para uma assinatura do Azure com sua conta organizacional, você já tem um locatário!  Em Olá [Portal do Azure](https://portal.azure.com), você deve encontrar um locatário quando você navega muito "Mais serviços" e "Do Azure Active Directory."  Você é livre toouse este locatário como você pode ver se ajustar.

## <a name="start-from-scratch"></a>Começar do zero
Se todos os Olá acima for tooyou sem sentido, não se preocupe.  Visite [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign para o Azure com uma nova organização.  Depois de concluir o processo de saudação, você terá seu próprio locatário do Azure AD com nome de domínio Olá escolhido durante a inscrição para cima.  Em Olá [Portal do Azure](https://portal.azure.com), você pode encontrar seu locatário, navegando muito "Azure Active Directory" no NAV. à esquerda de saudação

Como parte do processo de saudação de inscrever-se no Azure, será necessário tooprovide detalhes de cartão de crédito.  Você pode prosseguir com confiança - você não será cobrado para publicar aplicativos no AD do Azure nem para criar novos locatários.
