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
ms.openlocfilehash: 0c9a9a56e1489ee91fcc332beeef36cdc9c93dc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Sincronização em um domínio gerenciado dos Serviços de Domínio do Azure AD
O diagrama a seguir ilustra o funcionamento da sincronização nos domínios gerenciados dos Serviços de Domínio do Azure AD.

![Topologia de sincronização nos Serviços de Domínio do Azure AD](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-to-your-azure-ad-tenant"></a>Sincronização do diretório local para seu locatário do Azure AD
A sincronização do Azure AD Connect é usada para sincronizar contas de usuário, associações de grupo e hashes de credencial para seu locatário do Azure AD. Os atributos de contas de usuário, como o UPN e o SID (identificador de segurança) local são sincronizados. Se você usar os Serviços de Domínio do Azure AD, os hashes de credencial herdados necessários para a autenticação NTLM e Kerberos também serão sincronizados com seu locatário do Azure AD.

Se você configurar o write-back, as alterações que ocorrem em seu diretório do Azure AD serão sincronizadas com o Active Directory local. Por exemplo, se você alterar sua senha usando a funcionalidade de alteração de senha de autoatendimento do Azure AD, a senha alterada é atualizada em seu local de domínio do AD.

> [!NOTE]
> Sempre use a versão mais recente do Azure AD Connect para garantir que você tenha correções para todos os bugs conhecidos.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-to-your-managed-domain"></a>Sincronização do seu locatário do Azure AD para seu domínio gerenciado
As contas de usuário, as associações de grupo e os hashes de credenciais são sincronizados do seu locatário do Azure AD para seu domínio gerenciado dos Serviços de Domínio do Azure AD. Esse processo de sincronização é automático. Você não precisa configurar, monitorar ou gerenciar esse processo de sincronização. Após a conclusão da sincronização inicial do seu diretório, que só ocorre uma vez, geralmente demora cerca de 20 minutos para que as alterações feitas ao Azure AD sejam refletidas em seu domínio gerenciado. Esse intervalo de sincronização aplica-se a alterações de senha ou alterações em atributos feitos no Azure AD.

O processo de sincronização também é unidirecional por natureza. O domínio gerenciado é basicamente somente leitura, exceto qualquer OUs personalizadas que você criar. Portanto, você não pode fazer alterações em atributos de usuário, senhas de usuário ou associações de grupo do domínio gerenciado. Como resultado, não há nenhuma sincronização reversa de alterações do seu domínio gerenciado de volta para seu locatário do Azure AD.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Sincronização de um ambiente de várias florestas locais
Muitas organizações têm uma infraestrutura de identidade local bastante complexa que consiste em várias florestas de contas. O Azure AD Connect oferece suporte à sincronização de usuários, de grupos e de hashes de credencial de ambientes de várias florestas para seu locatário do Azure AD.

Por outro lado, o seu locatário do Azure AD é um namespace muito mais simples. Para permitir aos usuários acessar aplicativos protegidos pelo Azure AD de forma confiável, resolva os conflitos de UPN entre contas de usuário em diferentes florestas. Seu domínio gerenciado dos Serviços de Domínio do Azure AD é ligeiramente parecido com o seu locatário do Azure AD. Portanto, você verá uma estrutura de UO simples em seu domínio gerenciado. Todos os usuários e grupos são armazenados no contêiner 'Usuários AADDC', independentemente do domínio local ou da floresta na qual eles foram sincronizados. Talvez você tenha configurado uma estrutura de UO hierárquica local. No entanto, o domínio gerenciado ainda tem uma estrutura de UO simples.

## <a name="exclusions---what-isnt-synchronized-to-your-managed-domain"></a>Exclusões - o que não é sincronizado com o domínio gerenciado
Os seguintes atributos ou objetos não são sincronizados para seu locatário do Azure AD ou para seu domínio gerenciado:

* **Atributos excluídos:** você pode optar por excluir determinados atributos da sincronização para seu locatário do Azure AD do seu domínio local usando o Azure AD Connect. Esses atributos excluídos não estão disponíveis no seu domínio gerenciado.
* **Políticas de Grupo:** as políticas de grupo configuradas em seu domínio local não são sincronizadas com o domínio gerenciado.
* **Compartilhamento SYSVOL:** da mesma forma, o conteúdo do compartilhamento SYSVOL no domínio local não é sincronizado com o domínio gerenciado.
* **Objetos de computador:** objetos de computador dos computadores associados ao seu domínio local não são sincronizados com o seu domínio gerenciado. Esses computadores não têm uma relação de confiança com o domínio gerenciado e pertencem ao domínio local apenas. Em seu domínio gerenciado, você encontrará os objetos de computador somente para computadores que você ingressou explicitamente no domínio gerenciado.
* **Atributos SIDHistory para usuários e grupos:** os SIDs do usuário principal e do grupo primário do seu domínio local são sincronizados com seu domínio gerenciado. No entanto, os atributos SidHistory existentes para usuários e grupos não são sincronizados do seu domínio local para seu domínio gerenciado.
* **Estruturas de unidades organizacionais (UO):** as unidades organizacionais definidas em seu domínio local não serão sincronizadas ao seu domínio gerenciado. Há duas UOs internas em seu domínio gerenciado. Por padrão, o domínio gerenciado tem uma estrutura de UO simples. No entanto, você pode optar por [criar uma UO personalizada em seu domínio gerenciado](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-to-your-managed-domain"></a>Como os atributos específicos são sincronizados com o domínio gerenciado
A tabela a seguir lista alguns atributos comuns e descreve como eles serão sincronizados com o domínio gerenciado.

| O atributo em seu domínio gerenciado | Fonte | Observações |
|:--- |:--- |:--- |
| UPN |Atributo UPN do usuário no seu locatário do Azure AD |O atributo UPN do seu locatário do Azure AD é sincronizado como ele está para o domínio gerenciado. Portanto, a maneira mais confiável para entrar no seu domínio gerenciado é usando seu UPN. |
| SAMAccountName |O atributo mailNickname do usuário no seu locatário do Azure AD ou gerado automaticamente |O atributo SAMAccountName é originado do atributo mailNickname no seu locatário do Azure AD. Se várias contas de usuário tiverem o mesmo atributo mailNickname, SAMAccountName será gerado automaticamente. Se o mailNickname ou o prefixo UPN do usuário tiver mais de 20 caracteres, o SAMAccountName será gerado automaticamente para satisfazer o limite de 20 caracteres em atributos SAMAccountName. |
| Senhas |Senha do usuário do seu locatário do Azure AD |Os hashes de credenciais necessários para a autenticação NTLM ou Kerberos (também chamados de credenciais suplementares) são sincronizados do seu locatário do Azure AD. Se seu locatário do Azure AD for um locatário sincronizado, essas credenciais serão obtidas do seu domínio local. |
| SID do usuário/grupo primário |Gerado automaticamente |O SID primário para contas de usuário/grupo é gerado automaticamente no seu domínio gerenciado. Esse atributo não coincide com o SID do usuário/grupo primário do objeto em seu local de domínio do AD. Essa incompatibilidade ocorre porque o domínio gerenciado tem um namespace de SID diferente do seu domínio local. |
| Histórico de SID para usuários e grupos |SID de usuário e grupo primário local |O atributo SidHistory para usuários e grupos no domínio gerenciado é definido para corresponder ao SID do grupo ou usuário primário correspondente em seu domínio local. Esse recurso ajuda a facilitar o arrastar e deslocar de aplicativos no local para o domínio gerenciado, já que você não precisa reaplicar a ACL nos recursos. |

> [!NOTE]
> **Entrar para o domínio usando o formato UPN:** o atributo SAMAccountName pode ser gerado automaticamente para algumas contas de usuário em seu domínio gerenciado. Se vários usuários tiverem o mesmo atributo mailNickname ou os usuários tiverem prefixos UPN excessivamente longos, o SAMAccountName para esses usuários poderá ser gerado automaticamente. Portanto, o formato de SAMAccountName (por exemplo, ' CONTOSO100\pedrousuario') nem sempre é uma maneira confiável de entrar no domínio. O SAMAccountName gerado automaticamente dos usuários pode diferir do seu prefixo UPN. Use o formato UPN (por exemplo, 'joeuser@contoso100.com') para entrar no domínio gerenciado de forma confiável.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Mapeamento de atributos para contas de usuário
A tabela a seguir ilustra como os atributos específicos de objetos de usuário em seu locatário do Azure AD são sincronizados com os atributos correspondentes em seu domínio gerenciado.

| Atributo de usuário no seu locatário do Azure AD | Atributo de usuário em seu domínio gerenciado |
|:--- |:--- |
| accountEnabled |userAccountControl (define ou limpa o bit de ACCOUNT_DISABLED) |
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
| passwordPolicies |userAccountControl (define ou limpa o bit de DONT_EXPIRE_PASSWORD) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| sobrenome |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Mapeamento de atributo para grupos
A tabela a seguir ilustra como os atributos específicos de objetos de grupo em seu locatário do Azure AD são sincronizados com os atributos correspondentes em seu domínio gerenciado.

| Atributo de grupo em seu locatário do Azure AD | Atributo de grupo em seu domínio gerenciado |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (às vezes pode ser gerado automaticamente) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-to-your-azure-ad-tenant-from-your-managed-domain"></a>Objetos que não são sincronizados com seu locatário do Azure AD do seu domínio gerenciado
Conforme descrito em uma seção anterior deste artigo, há uma sincronização de seu domínio gerenciado para seu locatário do Azure AD. Você pode optar por [criar uma UO (unidade organizacional) personalizada](active-directory-ds-admin-guide-create-ou.md) em seu domínio gerenciado. Além disso, você pode criar outras OUs, usuários, grupos ou contas de serviço nessas OUs personalizadas. Nenhum dos objetos criados em OUs personalizadas é sincronizado de volta para seu locatário do Azure AD. Esses objetos estão disponíveis para uso somente dentro de seu domínio gerenciado. Portanto, esses objetos não são visíveis usando cmdlets do PowerShell do Azure AD, a API do Graph do Azure AD ou usando o interface do usuário de gerenciamento do Azure AD.

## <a name="related-content"></a>Conteúdo relacionado
* [Recursos – Azure AD Domain Services](active-directory-ds-features.md)
* [Cenários de implantação – Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Considerações de rede para Serviços de Domínio do Azure AD](active-directory-ds-networking.md)
* [Introdução aos Serviços de Domínio do Azure AD](active-directory-ds-getting-started.md)
