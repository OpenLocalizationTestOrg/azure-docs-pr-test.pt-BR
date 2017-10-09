---
title: "Sincronização do Azure AD Connect: Noções Básicas sobre Usuários e Contatos | Microsoft Docs"
description: "Explica usuários e contatos na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect Sync: noções básicas sobre usuários e contatos
Há vários motivos diferentes de por que existem várias florestas do Active Directory e várias topologias de implantação diferentes. Os modelos comuns incluem uma implantação do recurso em conta e florestas sincronizadas de GAL (Lista de Endereços Global) após uma fusão e aquisição. Mas mesmo que haja modelos puros, modelos híbridos são comuns também. configuração padrão de saudação na sincronização do Azure AD Connect não supõe qualquer modelo específico, mas dependendo de como a correspondência de usuário foi selecionado no guia de instalação do hello, comportamentos diferentes podem ser observados.

Neste tópico, veremos como configuração padrão de saudação se comporta em determinadas topologias. Percorreremos configuração hello e Olá Editor de regras de sincronização pode ser toolook usado na configuração de saudação.

Há algumas regras gerais Olá configuração pressupõe:

* Independentemente de qual ordenar importar do Active Directories de origem hello, resultado final de saudação sempre deve ser Olá mesmo.
* Uma conta ativa sempre também contribuirá com informações de logon, incluindo **userPrincipalName** e **sourceAnchor**.
* Uma conta desabilitada contribuirá com userPrincipalName e sourceAnchor, a menos que ele é uma caixa de correio vinculada, se não houver nenhum toobe conta ativa encontrado.
* Uma conta com uma caixa de correio vinculada nunca será usada para userPrincipalName e sourceAnchor. Pressupõe-se que uma conta ativa será encontrada posteriormente.
* Um objeto de contato pode ser provisionado tooAzure AD como um contato ou um usuário. Você realmente não sabe até que todas as florestas do Active Directory de origem sejam processadas.

## <a name="contacts"></a>Contatos
Ter contatos que representam um usuário em uma floresta diferente é comum após uma fusão e aquisição em que uma solução GALSync está fazendo a ponte entre duas ou mais florestas do Exchange. o objeto de contato Olá sempre ingressará a partir Olá conector espaço toohello metaverso usando o atributo de mensagem de saudação. Se já houver um objeto de contato ou um objeto de usuário com hello mesmo endereço de email, Olá objetos serão Unidos. Isso é configurado na regra Olá **no AD – ingresso do contato**. Também há uma regra denominada **no AD – contato comum** com um atributo de metaverso atributo fluxo toohello **sourceObjectType** com constante Olá **entre em contato com**. Essa regra tem precedência muito baixa se qualquer objeto do usuário é toohello ingressado no mesmo objeto de metaverso, então a regra Olá **em do AD – usuário comum** contribuirá com atributo de toothis de usuário de valor de saudação. Com essa regra, esse atributo terá valor Olá contato se nenhum usuário foi ingressado e Olá valor usuário se pelo menos um usuário foi encontrado.

Para o provisionamento de um objeto tooAzure AD, Olá regra de saída **Out tooAAD – ingresso de contato** criará um objeto de contato se hello atributo metaverso **sourceObjectType** está definido muito**entre em contato com** . Se esse atributo for definido muito**usuário**, em seguida, a regra de saudação **Out tooAAD – ingresso de usuário** criará um objeto de usuário, em vez disso.
É possível que um objeto seja promovido de contato tooUser quando mais Active Directories de origem são importados e sincronizados.

Por exemplo, em uma topologia GALSync encontraremos objetos de contato para todos na segunda floresta de saudação quando importarmos a primeira floresta de saudação. Isso preparará novos objetos de contato Olá conector AAD. Nós mais tarde quando importar e sincronizar floresta segundo Olá, vamos localizar Olá usuários reais e uni-los toohello objetos do metaverso existentes. Em seguida, vamos excluir o objeto de contato Olá no AAD e criar um novo objeto de usuário em vez disso.

Se você tiver uma topologia onde usuários são representados como contatos, certifique-se de que selecionar usuários toomatch no atributo de email Olá no guia de instalação de saudação. Se você selecionar outra opção, terá uma configuração dependente de pedido. Objetos de contato sempre ingressará no atributo de email Olá, mas os objetos de usuário só serão ingressados no atributo de mensagem de saudação se essa opção foi selecionada no guia de instalação de saudação. Você poderia terminar com dois objetos diferentes no metaverso Olá com hello mesmo atributo de email se o objeto de contato Olá foi importado antes do objeto de usuário hello. Durante a exportação tooAzure AD, um erro será gerado. Esse comportamento ocorre por design e pode indicar dados incorretos ou essa topologia Olá não foi corretamente identificada durante a instalação de saudação.

## <a name="disabled-accounts"></a>Contas desabilitadas
As contas desabilitadas também são sincronizadas tooAzure AD. As contas desabilitadas são recursos comuns de toorepresent no Exchange, como salas de conferência. exceção de saudação é usuários com uma caixa de correio vinculada; Como mencionado anteriormente, eles nunca provisionarão uma tooAzure conta AD.

suposição Olá é que, se uma conta de usuário desabilitada for encontrada, então não encontraremos outra conta ativa posteriormente e objeto Olá é provisionado tooAzure AD com hello userPrincipalName e sourceAnchor encontrados. Caso outra conta ativa ingresse toohello mesmo objeto de metaverso, então seu userPrincipalName e sourceAnchor será usado.

## <a name="changing-sourceanchor"></a>Alterando o sourceAnchor
Quando um objeto tiver sido exportado tooAzure AD, em seguida, ele não é permitido toochange Olá sourceAnchor mais. Quando o objeto de saudação foi o atributo do metaverso hello exportada **cloudSourceAnchor** é definido com hello **sourceAnchor** valor aceito pelo AD do Azure. Se **sourceAnchor** é alterado e não corresponder **cloudSourceAnchor**, regra Olá **Out tooAAD – ingresso de usuário** gerará o erro Olá **atributo sourceAnchor foi alterado**. Nesse caso, a saudação configuração ou os dados devem ser corrigidos Olá assim mesmo sourceAnchor esteja presente no metaverso Olá novamente antes de objeto Olá pode ser sincronizado novamente.

## <a name="additional-resources"></a>Recursos adicionais
* [Azure AD Connect Sync: personalizando opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

