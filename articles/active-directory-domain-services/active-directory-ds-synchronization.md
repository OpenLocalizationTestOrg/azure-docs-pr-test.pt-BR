---
title: "Azure Active Directory Domain Services: sincronização nos domínios gerenciados | Microsoft Docs"
description: "Compreender a sincronização em um domínio gerenciado do Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Sincronização em um domínio gerenciado dos Serviços de Domínio do Azure AD
Olá diagrama a seguir ilustra como a sincronização funciona nos serviços de domínio do AD do Azure domínios gerenciados.

![Topologia de sincronização nos Serviços de Domínio do Azure AD](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Sincronização do seu locatário de tooyour AD do Azure do diretório local
Sincronização do Azure AD Connect é toosynchronize usadas contas de usuário, associações de grupo e locatário de tooyour AD do Azure de hashes de credencial. Atributos de usuário de contas como Olá UPN e SID (identificador de segurança) são sincronizados no local. Se você usar os serviços de domínio do AD do Azure, hashes de credenciais herdados necessárias para a autenticação NTLM e Kerberos também são sincronizadas tooyour locatário de AD do Azure.

Se você configurar o write-back, alterações que ocorrem em seu diretório do AD do Azure são sincronizadas tooyour voltar do Active Directory local. Por exemplo, se você alterar sua senha usando recursos de alteração de senha de autoatendimento do AD do Azure, senha alterada Olá é atualizada em seu local de domínio do AD.

> [!NOTE]
> Use sempre a versão mais recente de saudação do Azure AD Connect tooensure tiver correções para todos os erros conhecidos.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Sincronização do seu tooyour de locatário do AD do Azure gerenciados domínio
Contas de usuário, associações de grupo e hashes de credencial são sincronizados do seu locatário de AD do Azure tooyour domínio gerenciado por serviços de domínio do AD do Azure. Esse processo de sincronização é automático. Você não precisa tooconfigure, monitorar e gerenciar esse processo de sincronização. Após a conclusão da saudação única a sincronização inicial de seu diretório, ele geralmente leva cerca de 20 minutos para que as alterações feitas no AD do Azure toobe refletidas no seu domínio gerenciado. Esse intervalo de sincronização se aplica alterações toopassword ou alterações tooattributes feitas no AD do Azure.

o processo de sincronização Olá é também uma-vias/unidirecional por natureza. O domínio gerenciado é basicamente somente leitura, exceto qualquer OUs personalizadas que você criar. Portanto, você não pode fazer alterações toouser atributos, as senhas de usuário ou associações de grupo no domínio gerenciado hello. Como resultado, não há nenhuma sincronização reversa de alterações do seu tooyour voltar do domínio gerenciado locatário do AD do Azure.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Sincronização de um ambiente de várias florestas locais
Muitas organizações têm uma infraestrutura de identidade local bastante complexa que consiste em várias florestas de contas. Conexão do AD do Azure oferece suporte a sincronização de usuários, grupos e hashes de credencial de locatário do AD do Azure de tooyour ambientes de várias florestas.

Por outro lado, o seu locatário do Azure AD é um namespace muito mais simples. tooenable usuários tooreliably acessar aplicativos protegidos pelo AD do Azure, resolva os conflitos UPN entre contas de usuário em florestas diferentes. Seu ursos de domínio gerenciados de serviços de domínio do AD do Azure fechar semelhança tooyour locatário do AD Azure. Portanto, você verá uma estrutura de UO simples em seu domínio gerenciado. Todos os usuários e grupos são armazenados no contêiner de 'Usuários AADDC' hello, independentemente do domínio no local de saudação ou floresta na qual eles foram sincronizados em. Talvez você tenha configurado uma estrutura de UO hierárquica local. No entanto, o domínio gerenciado ainda tem uma estrutura de UO simples.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Exclusões - não é sincronizado domínio gerenciado tooyour
Olá seguintes objetos ou atributos não são sincronizados tooyour locatário de AD do Azure ou domínio gerenciado tooyour:

* **Excluídos atributos:** poderá tooexclude determinados atributos da sincronização locatário tooyour AD do Azure do seu domínio local usando o Azure AD Connect. Esses atributos excluídos não estão disponíveis no seu domínio gerenciado.
* **Políticas de grupo:** políticas de grupo configuradas em seu domínio local não são domínio gerenciado tooyour sincronizados.
* **Compartilhamento do SYSVOL:** da mesma forma, o conteúdo de saudação do hello compartilhamento SYSVOL no seu domínio local não está domínio gerenciado tooyour sincronizados.
* **Objetos de computador:** objetos de computador do domínio dos computadores tooyour ingressado no local não são domínio gerenciado tooyour sincronizados. Esses computadores não têm uma relação de confiança com o domínio gerenciado e pertencem tooyour local apenas ao domínio. Seu domínio gerenciado, você encontrará os objetos de computador somente para computadores que têm toohello explicitamente ingressado no domínio gerenciados domínio.
* **Atributos de SidHistory para usuários e grupos:** usuário primário hello e grupo primário SIDs do seu domínio local são domínio gerenciado tooyour sincronizados. No entanto, os atributos de SidHistory existentes para usuários e grupos não são sincronizados do seu domínio gerenciado de tooyour de domínio local.
* **Estruturas de unidades (unidade Organizacional) da organização:** unidades organizacionais definidas em seu domínio local não sincronizar domínio gerenciado tooyour. Há duas UOs internas em seu domínio gerenciado. Por padrão, o domínio gerenciado tem uma estrutura de UO simples. No entanto poderá muito[criar uma UO personalizada no seu domínio gerenciado](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Como os atributos específicos são domínio gerenciado tooyour sincronizado
Olá, a tabela a seguir lista alguns atributos comuns e descreve como eles são o domínio gerenciado tooyour sincronizados.

| O atributo em seu domínio gerenciado | Fonte | Observações |
|:--- |:--- |:--- |
| UPN |Atributo UPN do usuário no seu locatário do Azure AD |atributo UPN de saudação do seu locatário do AD do Azure é sincronizado como domínio tooyour gerenciado. Portanto, Olá toosign de maneira mais confiável no domínio gerenciado tooyour está usando o UPN. |
| SAMAccountName |O atributo mailNickname do usuário no seu locatário do Azure AD ou gerado automaticamente |atributo de SAMAccountName Olá originado do atributo de mailNickname Olá em seu locatário do AD do Azure. Se várias contas de usuário tem Olá mesmo atributo de mailNickname, Olá SAMAccountName é gerado automaticamente. Se hello mailNickname ou prefixo UPN do usuário tiver mais de 20 caracteres, Olá SAMAccountName é gerado automaticamente toosatisfy Olá 20 caractere limite em atributos SAMAccountName. |
| Senhas |Senha do usuário do seu locatário do Azure AD |Os hashes de credenciais necessários para a autenticação NTLM ou Kerberos (também chamados de credenciais suplementares) são sincronizados do seu locatário do Azure AD. Se seu locatário do Azure AD for um locatário sincronizado, essas credenciais serão obtidas do seu domínio local. |
| SID do usuário/grupo primário |Gerado automaticamente |Olá o SID primário para contas de usuário/grupo é gerado automaticamente em seu domínio gerenciado. Esse atributo não coincide com hello principal usuário/grupo SID do objeto de saudação em seus locais de domínio do AD. Essa incompatibilidade ocorre porque o domínio gerenciado Olá tem um namespace diferente do SID de domínio local. |
| Histórico de SID para usuários e grupos |SID de usuário e grupo primário local |atributo de SidHistory Olá para usuários e grupos em seu domínio gerenciado é definido usuário primário do toomatch Olá correspondente ou SID de grupo em seu domínio local. Esse recurso ajuda a tornar levantar shift e do local aplicativos toohello domínio gerenciado mais fácil, pois você não precisa de recursos de toore ACL. |

> [!NOTE]
> **Entrar toohello domínio gerenciado usando o formato UPN Olá:** atributo de SAMAccountName Olá pode ser gerada automaticamente para algumas contas de usuário em seu domínio gerenciado. Se vários usuários têm Olá mesmo atributo mailNickname ou usuários excessivamente longo UPN prefixos, Olá SAMAccountName para esses usuários pode ser geradas automaticamente. Portanto, formato de SAMAccountName hello (por exemplo, ' CONTOSO100\joeuser') não é sempre um toosign de maneira confiável no domínio toohello. O SAMAccountName gerado automaticamente dos usuários pode diferir do seu prefixo UPN. Use o formato de UPN hello (por exemplo, 'joeuser@contoso100.com') toosign em toohello gerenciados domínio confiável.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Mapeamento de atributos para contas de usuário
Olá, a tabela a seguir ilustra a atributos específicos para objetos de usuário no seu locatário do AD do Azure são sincronizados toocorresponding atributos no seu domínio gerenciado.

| Atributo de usuário no seu locatário do Azure AD | Atributo de usuário em seu domínio gerenciado |
|:--- |:--- |
| accountEnabled |userAccountControl (define ou limpa Olá ACCOUNT_DISABLED bit) |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |título |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (às vezes pode ser gerado automaticamente) |
| Serviço Móvel |Serviço Móvel |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (define ou limpa Olá DONT_EXPIRE_PASSWORD bit) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| sobrenome |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Mapeamento de atributo para grupos
Olá, a tabela a seguir ilustra a atributos específicos para objetos de grupo no seu locatário do AD do Azure são sincronizados toocorresponding atributos no seu domínio gerenciado.

| Atributo de grupo em seu locatário do Azure AD | Atributo de grupo em seu domínio gerenciado |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (às vezes pode ser gerado automaticamente) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Objetos que não estão sincronizados tooyour locatário de AD do Azure do seu domínio gerenciado
Conforme descrito em uma seção anterior deste artigo, não há nenhuma sincronização do seu tooyour voltar do domínio gerenciado locatário do AD do Azure. Você pode escolher muito[criar um personalizado UO (unidade organizacional)](active-directory-ds-admin-guide-create-ou.md) em seu domínio gerenciado. Além disso, você pode criar outras OUs, usuários, grupos ou contas de serviço nessas OUs personalizadas. Nenhum dos objetos Olá criados OUs personalizadas são sincronizados tooyour back locatário de AD do Azure. Esses objetos estão disponíveis para uso somente dentro de seu domínio gerenciado. Portanto, esses objetos não são visíveis usando cmdlets do PowerShell do Azure AD, Azure AD Graph API ou usando a IU de gerenciamento de saudação do AD do Azure.

## <a name="related-content"></a>Conteúdo relacionado
* [Recursos – Azure AD Domain Services](active-directory-ds-features.md)
* [Cenários de implantação – Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Considerações de rede para Serviços de Domínio do Azure AD](active-directory-ds-networking.md)
* [Introdução aos Serviços de Domínio do Azure AD](active-directory-ds-getting-started.md)
