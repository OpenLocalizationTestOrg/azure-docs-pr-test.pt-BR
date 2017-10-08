---
title: "Tópicos de Ajuda do Portal de registro de aaaApp | Microsoft Docs"
description: "Uma descrição de vários recursos no portal de registro de aplicativo hello Microsoft."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Referência de registro de aplicativo
Este documento fornece contexto e descrições dos vários recursos no hello Portal de registro de aplicativo do Microsoft [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Meus Aplicativos
Essa lista contém todos os aplicativos registrados para uso com o ponto de extremidade do hello AD do Azure v 2.0.  Esses aplicativos têm Olá capacidade toosign os usuários com as duas contas pessoais da conta da Microsoft e contas de trabalho/escola do Active Directory do Azure.  toolearn mais sobre o ponto de extremidade de v 2.0 Olá AD do Azure, consulte nosso [visão geral de v 2.0](active-directory-appmodel-v2-overview.md).  Esses aplicativos também podem ser usado toointegrate com extremidade para autenticação de conta do Microsoft hello, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Aplicativos do Live SDK
Esta lista contém todos os aplicativos registrados para uso exclusivo com uma conta da Microsoft.  Eles não são habilitados para uso com o Azure Active Directory ou outro.  Isso é onde você encontrará todos os aplicativos que tenha sido registrados com o portal do desenvolvedor MSA Olá em `https://account.live.com/developers/applications`.  Todas as funções executadas anteriormente em `https://account.live.com/developers/applications` podem ser executadas agora nesse novo portal, `https://apps.dev.microsoft.com`.  Se você tiver outras perguntas sobre seus aplicativos da conta da Microsoft, entre em contato conosco.

## <a name="application-secrets"></a>Segredos do aplicativo
Segredos do aplicativo são credenciais que permitem que seu aplicativo tooperform confiável [autenticação de cliente](http://tools.ietf.org/html/rfc6749#section-2.3) com o Azure AD.  OAuth & OpenID Connect, segredos de um aplicativo é normalmente chamados tooas um `client_secret`.  No protocolo de v 2.0 hello, qualquer aplicativo que recebe um token de segurança em um local endereçável da web (usando um `https` esquema) deve usar um tooidentify de segredo do aplicativo em si tooAzure AD após resgate esse token de segurança.  Além disso, qualquer cliente nativo que recebe tokens em um dispositivo serão proibidos de usar uma autenticação de cliente de tooperform segredo do aplicativo, toodiscourage Olá armazenamento de segredos em ambientes inseguras.

Cada aplicativo pode conter dois segredos do aplicativo válidos em qualquer momento.  Ao manter dois segredos, você tem Olá ablilty tooperform periódica substituição de chave em todo o ambiente do seu aplicativo.  Depois de migrar toda Olá o novo segredo do aplicativo tooa, você pode excluir o antigo segredo do hello e provisionar um novo.

Neste momento, apenas dois tipos de segredos do aplicativo são permitidos no portal de registro de aplicativo hello.  Escolhendo **gerar nova senha** irá gerar e armazenar um segredo compartilhado no repositório de dados do respectivos hello, que você pode usar em seu aplicativo.  Escolhendo **gerar novo par de chaves** criará um novo par de chaves de pública/privada que pode ser baixado e usado para autenticação de cliente tooAzure AD.

## <a name="profile"></a>Perfil
seção de perfil de saudação do portal de registro de aplicativo hello pode ser usado toocustomize Olá logon na página do seu aplicativo.  Neste momento, você pode alterar o logotipo do aplicativo da página, os termos de privacidade e URL do serviço de entrada hello.  Olá logotipo deve ser uma imagem de pixel de 48 x 48 ou 50 x 50 transparente em um arquivo GIF, PNG ou JPEG 15 KB ou menos.  Tente alterar valores de saudação e exibindo Olá resultando na página de entrada!

## <a name="live-sdk-support"></a>Suporte ao Live SDK
Quando você ativar "Live SDK suporte", qualquer aplicativo segredos que você criar serão provisionados no hello AD do Azure e os dados da Microsoft Account armazena.  Isso permitirá que seu toointegrate aplicativo diretamente com hello serviço Account da Microsoft (login.live.com).  Se você desejar toobuild um aplicativo usando o Microsoft Account diretamente (como ponto de extremidade de toousing contrário Olá AD do Azure v 2.0), você deve garantir que o suporte do SDK ao vivo está habilitado.

Desabilitar o suporte do SDK do Live garantirá que segredo do aplicativo hello é apenas gravado no repositório de dados de saudação do AD do Azure.  repositório de dados de saudação do AD do Azure incorpora normas de classe empresarial que permitem toomeet determinados padrões, como conformidade FISMA.  Se você habilitar o suporte ao Live SDK, talvez seu aplicativo não fique em conformidade com alguns desses padrões.

Se você planeja se apenas o ponto de extremidade do toouse Olá AD do Azure versão 2.0, você pode desativar com segurança suporte Live SDK.

