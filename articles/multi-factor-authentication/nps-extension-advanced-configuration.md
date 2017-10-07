---
title: "Olá aaaConfigure extensão do Azure MFA NPS | Microsoft Docs"
description: "Depois de instalar a extensão NPS hello, siga estas etapas para configuração avançada como lista branca IP e a substituição de UPN."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Opções de configuração para Olá extensão NPS para autenticação multifator avançada

Olá extensão do servidor de diretivas de rede (NPS) estende os recursos de autenticação multifator do Azure baseado em nuvem para sua infraestrutura local. Este artigo pressupõe que você já tiver instalado de extensão de saudação e agora deseja tooknow como extensão de saudação toocustomize para que você precisa. 

## <a name="alternate-login-id"></a>ID de logon alternativa

Como Olá extensão NPS conecta tooboth seu local e nuvem diretórios, você pode encontrar um problema onde o seu local nomes UPN (UPNs) não correspondem aos nomes de Olá na nuvem hello. toosolve esse problema, o uso de IDs de logon alternativo. 

Dentro de Olá extensão do NPS, você pode designar um toobe de atributo do Active Directory usado no lugar de saudação UPN para o Azure multi-Factor Authentication. Isso permite que você tooprotect seus recursos locais com a verificacao sem modificar seu UPNs locais. 

tooconfigure de logon alternativo IDs, ir muito`HKLM\SOFTWARE\Microsoft\AzureMfa` e editar Olá valores do registro a seguir:

| Nome | Tipo | Valor padrão | Descrição |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | string | Vazio | Designe um nome de saudação do atributo do Active Directory que você deseja toouse em vez da saudação UPN. Este atributo é usado como atributo de AlternateLoginId hello. Se esse valor do registro é definida tooa [atributo válido do Active Directory](https://msdn.microsoft.com/library/ms675090.aspx) (por exemplo, email ou displayName), em seguida, Olá valor do atributo é usado no lugar de UPN do usuário Olá para autenticação. Se esse valor do registro está vazio ou não configurado, então AlternateLoginId está desabilitado e UPN saudação do usuário é usado para autenticação. |
| LDAP_FORCE_GLOBAL_CATALOG | Booliano | Falso | Use este sinalizador tooforce saudação do Catálogo Global para pesquisas LDAP ao procurar AlternateLoginId. Configurar um controlador de domínio como um Catálogo Global, adicione Olá AlternateLoginId atributo toohello Catálogo Global e, em seguida, habilite esse sinalizador. <br><br> Se LDAP_LOOKUP_FORESTS estiver configurado (não estiver vazia), **esse sinalizador é imposto como true**, independentemente do valor de saudação da configuração de registro de saudação. Nesse caso, Olá extensão NPS requer Olá toobe de Catálogo Global configurado com o atributo de AlternateLoginId Olá para cada floresta. |
| LDAP_LOOKUP_FORESTS | string | Vazio | Forneça uma lista de ponto e vírgula separada de florestas toosearch. Por exemplo, *contoso.com;foobar.com*. Se esse valor do registro estiver configurado, Olá extensão NPS iterativamente pesquisa todas as florestas de saudação na ordem de saudação em que foram listados e retorna o primeiro valor de AlternateLoginId bem-sucedida hello. Se esse valor do registro não estiver configurado, pesquisa de AlternateLoginId Olá é domínio atual toohello restrita.|

Olá recomendado etapas para usar o tootroubleshoot problemas com IDs de logon alternativo [alternativa erros de ID de logon](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>Exceções de IP

Se você precisar de disponibilidade do servidor toomonitor, como se a balanceadores de carga verifique se os servidores que estão executando antes do envio de cargas de trabalho, você não quer essas toobe verificações bloqueada por solicitações de verificação. Em vez disso, crie uma lista de endereços IP que você saiba que são usados por contas de serviço e desabilite os requisitos de Autenticação Multifator para essa lista. 

tooconfigure uma lista de permissões de IP, vá muito`HKLM\SOFTWARE\Microsoft\AzureMfa` e configurar Olá valor do registro a seguir: 

| Nome | Tipo | Valor padrão | Descrição |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | string | Vazio | Forneça uma lista separada por ponto e vírgula de endereços IP. Inclua Olá endereços IP de máquinas de solicitações de serviço de origem, como Olá servidor NAS/VPN. Os intervalos IP que são sub-redes não têm suporte. <br><br> Por exemplo, *10.0.0.1;10.0.0.2;10.0.0.3*.

Quando uma solicitação chega de um endereço IP que existe na lista branca de hello, verificação em duas etapas é ignorada. Olá, lista branca de IPS é toohello em comparação com o endereço IP que é fornecido no hello *ratNASIPAddress* atributo de solicitação do RADIUS hello. Se uma solicitação RADIUS chega sem atributo de ratNASIPAddress hello, Olá aviso a seguir será registrado: "Lista branca de P_WHITE_LIST_WARNING::IP está sendo ignorada como o IP de origem está ausente na solicitação do RADIUS no atributo NasIpAddress."

## <a name="next-steps"></a>Próximas etapas

[Resolver mensagens de erro de saudação extensão NPS para o Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
