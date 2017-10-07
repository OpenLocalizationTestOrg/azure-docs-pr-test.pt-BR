---
title: AAA um erro inesperado ao executar o aplicativo do consentimento tooan | Microsoft Docs
description: "Discute os erros que podem ocorrer durante o processo de saudação de consentimento tooan aplicativo e que você pode fazer sobre eles"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Erro inesperado ao executar o aplicativo de tooan de consentimento

Este artigo aborda os erros que podem ocorrer durante o processo de saudação do aplicativo de tooan consentimento. Se você estiver procurando Solucionar Problemas de solicitações de consentimentos inesperados que não contêm mensagens de erro, consulte [Cenários de Autenticação do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Muitos aplicativos que se integram com o Active Directory do Azure exigem permissões tooaccess outros recursos em ordem toofunction. Quando esses recursos também são integrados com o Active Directory do Azure, tooaccess permissões eles geralmente é solicitada usando Olá comuns consentimento do framework. 

Isso resulta em um prompt de consentimento que está sendo exibido, que geralmente ocorre Olá primeira vez que um aplicativo é usado, mas também pode ocorrer em um uso subsequente do aplicativo hello.

Certas condições devem ser verdadeiras para um usuário tooconsent toohello permissões que um aplicativo requer. Se essas condições não forem atendidas, vários erros podem ocorrer. Estão incluídos:

## <a name="requesting-not-authorized-permissions-error"></a>Solicitação de erro de permissão não autorizada
* **AADSTS90093:** &lt;clientAppDisplayName&gt; está solicitando uma ou mais permissões que não estão autorizados toogrant. Contate um administrador, o que pode obter o consentimento toothis aplicativo em seu nome.

Esse erro ocorre quando um usuário que não seja um administrador da empresa tenta toouse um aplicativo que está solicitando permissões que somente um administrador pode conceder. Esse erro pode ser resolvido por um administrador concedendo acesso toohello aplicativo em nome de sua organização.

## <a name="policy-prevents-granting-permissions-error"></a>Política impede concessão de permissões de erro
* **AADSTS90093:** um administrador do &lt;tenantDisplayName&gt; definiu uma política que impede que você conceda &lt;nome do aplicativo&gt; Olá permissões está solicitando. Entre em contato com o administrador de &lt;tenantDisplayName&gt;, que pode conceder permissões toothis aplicativo em seu nome.

Esse erro ocorre quando um administrador da empresa desativa a capacidade de saudação para usuários tooconsent tooapplications, em seguida, um usuário não administrador tenta toouse um aplicativo que requer o consentimento. Esse erro pode ser resolvido por um administrador concedendo acesso toohello aplicativo em nome de sua organização.

## <a name="intermittent-problem-error"></a>Erro de problema intermitente
* **AADSTS90090:** parece que encontramos um problema intermitente gravação permissões Olá tentativa toogrant muito&lt;clientAppDisplayName&gt;. tente novamente mais tarde.

Esse erro indica que ocorreu um erro de serviço intermitente. Ele pode ser resolvido por tentativa de aplicativo de toohello tooconsent novamente.

## <a name="resource-not-available-error"></a>Erro de recurso não disponível
* **AADSTS65005:** aplicativo hello &lt;clientAppDisplayName&gt; solicitadas permissões tooaccess um recurso &lt;resourceAppDisplayName&gt; que não está disponível. 

Contate o desenvolvedor do aplicativo hello.

##  <a name="resource-not-available-in-tenant-error"></a>Recurso não disponível no erro do locatário
* **AADSTS65005:** &lt;clientAppDisplayName&gt; está solicitando acesso tooa recurso &lt;resourceAppDisplayName&gt; que não está disponível em sua organização &lt; tenantDisplayName&gt;. 

Certifique-se de que esse recurso está disponível ou contate o administrador de &lt;NomeExibiçãoLocatário&gt;.

## <a name="permissions-mismatch-error"></a>Erro de incompatibilidade de permissões
* **AADSTS65005:** aplicativo hello solicitado consentimento tooaccess recurso &lt;resourceAppDisplayName&gt;. A solicitação falhou porque não corresponde a como aplicativo hello foi previamente configurado durante o registro do aplicativo. Entre em contato com hello aplicativo vendor.* *

Estes erros todos ocorrem quando o aplicativo hello um usuário está tentando toois tooconsent solicitando permissões tooaccess um aplicativo de recurso que não pode ser encontrado no diretório da organização da saudação (Locatário). Isso pode ocorrer por vários motivos:

-   desenvolvedor de aplicativos de cliente Olá tiver configurado seu aplicativo incorretamente, causando toorequest acesso tooan inválido do recurso. Nesse caso, desenvolvedor do aplicativo hello deve atualizar Olá configuração de saudação cliente aplicativo tooresolve esse problema.

-   Uma entidade de serviço que representa o aplicativo de recurso de destino hello não existe na organização hello, ou existia no hello anterior, mas foi removida. tooresolve esse problema, uma entidade de serviço para o aplicativo de recurso hello deve ser provisionado na organização Olá para que o aplicativo de cliente hello pode solicitar permissões tooit. Isso pode acontecer em um número de maneiras, dependendo do tipo de saudação do aplicativo, incluindo:

    -   Adquirindo uma assinatura para o aplicativo de recurso hello (Microsoft aplicativos publicados)

    -   Aplicativo de recurso toohello consentimento

    -   Concedendo permissões de aplicativo hello via Olá Portal do Azure

    -   Adicionar o aplicativo hello de saudação Galeria de aplicativos do Azure AD

## <a name="next-steps"></a>Próximas etapas 

[Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Escopos, permissões e consentimento de saudação do Active Directory do Azure (ponto de extremidade v 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


