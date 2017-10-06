---
title: "atributos de sombra de serviço de sincronização do aaaAzure AD Connect | Microsoft Docs"
description: "Descreve como os atributos sombra funcionam no serviço de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Atributos sombra do serviço de sincronização do Azure AD Connect
A maioria dos atributos são representados Olá mesma maneira no AD do Azure como estão no Active Directory local. Mas alguns atributos têm algum tratamento especial e o valor do atributo Olá no AD do Azure pode ser diferente do que sincroniza o Azure AD Connect.

## <a name="introducing-shadow-attributes"></a>Introdução aos atributos sombra
Alguns atributos têm duas representações no Azure AD. Valor de local de saudação e um valor calculado são armazenadas. Esses atributos adicionais são chamados de atributos sombra. Olá dois atributos mais comuns em que você pode ver esse comportamento são **userPrincipalName** e **proxyAddress**. Olá alterações em valores de atributos ocorre quando há valores nesses atributos que representam domínios não verificados. Mas o mecanismo de sincronização de saudação em conectar lê Olá valor no atributo de sombra Olá isso da sua perspectiva, o atributo de saudação foi confirmado pelo AD do Azure.

Não é possível ver os atributos de sombra hello usando Olá portal do Azure ou com o PowerShell. Mas o conceito de saudação Noções básicas sobre ajuda tootroubleshoot você determinados cenários onde o atributo de saudação tem valores diferentes no local e na nuvem de saudação.

toobetter compreender o comportamento de hello, veja este exemplo da Fabrikam:  
![Domínios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Eles têm vários sufixos UPN no Active Directory local, mas verificaram apenas um.

### <a name="userprincipalname"></a>userPrincipalName
Um usuário tem Olá valores de atributo em um domínio não verificado a seguir:

| Atributo | Valor |
| --- | --- |
| userPrincipalName local | lee.sperry@fabrikam.com |
| shadowUserPrincipalName do Azure AD | lee.sperry@fabrikam.com |
| userPrincipalName do Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

atributo de userPrincipalName Olá é o valor de saudação que consulte ao usar o PowerShell.

Como valor do atributo Olá local real é armazenado no AD do Azure, quando você verificar o domínio fabrikam.com de Olá, AD do Azure atualiza o atributo userPrincipalName de saudação com valor de saudação do hello shadowUserPrincipalName. Você não tem toosynchronize as alterações do Azure AD Connect para esses toobe valores atualizados.

### <a name="proxyaddresses"></a>proxyAddresses
Olá mesmo processo para incluir somente os domínios verificados também ocorre proxyAddresses, mas com lógica adicional. seleção de saudação para domínios verificados ocorre apenas para usuários de caixa de correio. Um usuário habilitado para email ou contato representar um usuário em outra organização do Exchange e você pode adicionar todos os valores em objetos de toothese proxyAddresses.

Para um usuário de caixa de correio, no local ou no Exchange Online, somente os valores de domínios verificados são exibidos. O resultado pode ser este:

| Atributo | Valor |
| --- | --- |
| proxyAddresses local | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| proxyAddresses do Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

Nesse caso, **smtp:abbie.spencer@fabrikam.com** foi removido, pois esse domínio não foi verificado. Mas o Exchange também adicionou **SIP:abbie.spencer@fabrikamonline.com**. A Fabrikam não usou o Lync/Skype local, mas o Azure AD e o Exchange Online se preparam para isso.

Essa lógica para proxyAddresses é chamado tooas **ProxyCalc**. ProxyCalc é invocado a cada alteração em um usuário, quando:

- usuário Olá recebeu um plano de serviço que inclui o Exchange Online, mesmo se o usuário Olá não licenciado para o Exchange. Por exemplo, se o usuário Olá é atribuído Olá Office E3 SKU, mas só foi atribuído o SharePoint Online. Isso será verdadeiro mesmo se sua caixa de correio ainda for local.
- Olá msExchRecipientTypeDetails de atributo tem um valor.
- Você faz uma alteração tooproxyAddresses ou o userPrincipalName.

ProxyCalc pode levar algum tempo tooprocess uma alteração em um usuário e não é síncrono com o processo de exportação hello Azure AD Connect.

> [!NOTE]
> Olá ProxyCalc lógica tem alguns comportamentos adicionais para cenários avançados não são documentados neste tópico. Este tópico é fornecido para você toounderstand Olá comportamento e não toda a lógica interna de documento.

### <a name="quarantined-attribute-values"></a>Valores de atributo em quarentena
Os atributos sombra também são usados quando há valores de atributo duplicados. Para saber mais, veja [resiliência de atributo duplicada](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Consulte também
* [Sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md).
