---
title: "aaaLinks na página de saudação não funcionam para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: Como tootroubleshoot problemas com links quebrados em aplicativos de Proxy de aplicativo que foram integrados ao AD do Azure
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Links na página de saudação não funcionam para um aplicativo de Proxy de aplicativo

Este artigo ajuda tootroubleshoot por que os links em seu aplicativo de Proxy de aplicativo do Azure Active Directory não funcionam corretamente.

## <a name="overview"></a>Visão geral 
Depois de publicar um aplicativo de Proxy de aplicativo, links de somente Olá trabalho por padrão no aplicativo hello são toodestinations links contidos Olá publicados URL raiz. Olá links em aplicativos de saudação não estão funcionando, a URL interna Olá para o aplicativo hello provavelmente não inclui todos os destinos de saudação de links no aplicativo hello.

**Por que isso acontece?** Ao clicar em um link em um aplicativo, o URL do Proxy de aplicativo tentativas tooresolve hello como uma URL interna no Olá mesmo aplicativo, ou como uma URL disponível externamente. Se tooan URL interna que não está dentro de pontos de link Olá Olá mesmo aplicativo, ele não pertencer tooeither desses buckets e resultam em um erro não foi encontrado.

## <a name="ways-you-can-resolve-broken-links"></a>Maneiras de resolver links desfeitos

Há três tooresolve de maneiras esse problema. Opções de saudação abaixo estão em listados no aumento da complexidade.

1.  Certifique-se de que saudação a URL interna é uma pasta raiz que contém todos os links de saudação relevantes para o aplicativo hello. Isso permite que todos os toobe links resolvido conforme o conteúdo publicado no hello mesmo aplicativo.

    Se você alterar a URL interna Olá, mas não quiser Olá toochange página usuários inicial, alteração Olá URL da Home page toohello publicado anteriormente URL interna. Isso pode ser feito indo muito "Active Directory do Azure" -&gt; registros do aplicativo -&gt; selecione aplicativo hello -&gt; propriedades. Nessa guia Propriedades, consulte o campo hello "URL da página inicial" que você pode ajustar toobe Olá desejado na página inicial.

2.  Se seus aplicativos usam nomes de domínio totalmente qualificados (FQDNs), use [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish seus aplicativos. Esse recurso permite Olá mesmo toobe de URL usado interna e externamente.

    Essa opção garante que o hello links em seu aplicativo estejam acessíveis por meio do Proxy de aplicativo como links Olá Olá aplicativo toointernal URLs também são reconhecidos externamente. Observe que todos os links ainda precisam toobelong tooa aplicativo publicado. No entanto, com hello essa opção links não é necessário toobelong toohello mesmo aplicativo e pode pertencer toomultiple aplicativos.

3.  Se nenhuma dessas opções for viável, você unir visualização Olá para um novo recurso que fazer conversão/regravação de URL. Com essa opção, interno URLs ou links que existem no corpo de saudação HTML dos aplicativos será convertido, ou "mapeados", toohello publicado URLs externas de Proxy de aplicativo. Isso funciona somente para links em Olá HTML ou CSS, e isso não ajuda se o link é gerado pelo JS. 

Como resultado, é altamente recomendável usar Olá [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solução se possível. Se você deseja visualizar de saudação toojoin, email < aadapfeedback@microsoft.com > com applicationId(s) hello.

## <a name="next-steps"></a>Próximas etapas
[Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md)

