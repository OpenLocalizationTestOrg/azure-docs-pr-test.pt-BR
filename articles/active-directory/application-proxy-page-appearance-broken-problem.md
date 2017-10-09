---
title: "página aaaApplication não será exibido corretamente para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: "Diretrizes de quando a página de saudação não estiver exibindo corretamente em um aplicativo de Proxy de aplicativo integrado com o Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Página de aplicativo não exibe corretamente para um aplicativo de Proxy de aplicativo

Este artigo ajuda tootroubleshoot problemas com aplicativos de Proxy de aplicativo do Azure Active Directory quando você navegar toohello página, mas algo na página de saudação não parece estar correto.

## <a name="overview"></a>Visão geral
Quando você publica um aplicativo de Proxy de aplicativo, somente as páginas em sua raiz são acessíveis ao acessar o aplicativo hello. Se a página de saudação não estiver exibindo corretamente, Olá raiz URL interna usada para o aplicativo hello pode estar faltando alguns recursos da página. tooresolve, verifique se você publicou *todos os* Olá recursos para página hello como parte do seu aplicativo.

Você pode verificar esse é o problema de saudação abrindo o controlador de rede (como o Fiddler ou F12 ferramentas no Internet Explorer/borda), carregar página hello e procurando 404 erros. Que indica as páginas de saudação que atualmente não podem ser encontradas e talvez ainda precise toobe publicado.

Como um exemplo de nesse caso, suponha que você tenha publicado um aplicativo de despesas usando uma URL interna de <http://myapps/expenses>, mas usa o aplicativo hello folha de estilos de saudação <http://myapps/style.css>. Nesse caso, Olá folha de estilos não está publicada no seu aplicativo, para carregar o aplicativo de despesas Olá lançar um erro 404 ao tentar tooload Style. CSS. Neste exemplo, o problema de Olá deve ser resolvido publicando o aplicativo hello com uma URL interna de <http://myapp/> em vez disso.

## <a name="problems-with-publishing-as-one-application"></a>Problemas com a publicação como um aplicativo

Se não for possível toopublish Olá a todos os recursos no mesmo aplicativo, você precisa toopublish vários aplicativos e habilitar links entre eles.

toodo assim, recomendamos o uso de saudação [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solução. No entanto, essa solução requer que você possui o certificado de saudação para seu domínio e seus aplicativos usam nomes de domínio totalmente qualificados (FQDNs). Para outras opções, consulte Olá [solucionar problemas de links desfeitos documentação](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Próximas etapas
[Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure](application-proxy-publish-azure-portal.md)
