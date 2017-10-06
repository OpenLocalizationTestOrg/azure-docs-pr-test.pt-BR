---
title: aaaCustomizing mapeamentos de atributos do AD do Azure | Microsoft Docs
description: "Saiba quais mapeamentos de atributo para aplicativos SaaS no Azure Active Directory são como você pode modificá-las tooaddress sua empresa precisa."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Personalizar os mapeamentos de atributos de provisionamento de usuário para aplicativos SaaS no Azure Active Directory
AD do Microsoft Azure oferece suporte para aplicativos SaaS de terceiros toothird, como Salesforce, Google Apps e outros usuários de provisionamento do usuário. Se você tiver o provisionamento de um aplicativo SaaS de terceiros habilitado do usuário, Olá Portal de gerenciamento do Azure controla seus valores de atributo na forma de uma configuração chamada "mapeamento de atributo".

Há um conjunto predefinido de mapeamentos de atributo entre objetos de usuário do AD do Azure e objetos de usuário de cada aplicativo SaaS. Alguns aplicativos gerenciam outros tipos de objetos, como grupos ou contatos. <br> 
 Você pode personalizar mapeamentos de atributos padrão de saudação de acordo com as necessidades de negócios de tooyour. Isso significa que você pode alterar ou excluir mapeamentos de atributo existentes ou criar novos mapeamentos de atributo.

No portal de saudação do AD do Azure, você pode acessar esse recurso clicando em um **mapeamentos** configuração em **provisionamento** em Olá **gerenciar** seção de um  **Aplicativo corporativo**.


![Salesforce][5] 

Clicar em um **mapeamentos** configuração, abre Olá relacionada **mapeamento de atributo** folha.  
Não há mapeamentos de atributos que são exigidos por um toofunction de aplicativos SaaS corretamente. Para atributos obrigatórios, Olá **excluir** recurso não está disponível.


![Salesforce][6]  

O exemplo hello acima, você pode ver que Olá **Username** atributo de um objeto gerenciado no Salesforce é preenchido com hello **userPrincipalName** valor da saudação vinculado objeto do Active Directory do Azure.

Você pode personalizar os **Mapeamentos de Atributo** existentes clicando em um mapeamento. Isso abre o hello **Editar atributo** folha.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Noções básicas sobre tipos de mapeamento de atributo
Com mapeamentos de atributo, você controla como os atributos são preenchidos em um aplicativo SaaS de terceiro. Há quatro tipos diferentes de mapeamento com suporte:

* **Direto** – o atributo de destino Olá é populado com valor de saudação de um atributo do objeto vinculado Olá no AD do Azure.
* **Constante** – o atributo de destino Olá é preenchido com uma cadeia de caracteres específica que você especificou.
* **Expressão** -atributo de destino de saudação é preenchido com base no resultado de saudação de uma expressão como script. 
  Para saber mais, consulte [Escrever expressões para mapeamentos de atributo no Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Nenhum** -Olá atributo de destino é deixado sem modificações. No entanto, se o atributo de destino Olá estiver vazio, ele é preenchido com o valor de padrão de saudação que você especificar.

Em tipos de mapeamento de atributo básico de toothese quatro adição, mapeamentos de atributos personalizados suportam o conceito de saudação do opcional **padrão** atribuição de valor. atribuição de valor saudação padrão garante que um atributo de destino é preenchido com um valor se não houver nenhum valor no AD do Azure nem no objeto de destino de saudação. Olá a configuração mais comum é tooleave em branco.


## <a name="understanding-attribute-mapping-properties"></a>Noções básicas de propriedades de mapeamento de atributo

Na seção anterior do hello, você já foram introduzidas toohello propriedade de tipo de mapeamento de atributo.
Na propriedade de toothis adição, mapeamentos de atributo também dão suporte a saudação seguintes atributos:

- **Atributo de origem** -atributo de usuário de saudação do sistema de origem da saudação (por exemplo: Active Directory do Azure).
- **Atributo de destino** – atributo de usuário Olá no sistema de destino da saudação (por exemplo: ServiceNow).
- **Correspondem a objetos que usam esse atributo** – se este mapeamento deve ser usado ou não toouniquely identificar usuários entre sistemas de origem e destino hello. Isso normalmente é definido em Olá userPrincipalName ou atributo de email no AD do Azure, que geralmente é mapeada tooa campo de nome de usuário em um aplicativo de destino.
- **Precedência de correspondência** – vários atributos de correspondência podem ser definidos. Quando houver vários, elas são avaliadas na ordem Olá definido por este campo. Assim que uma correspondência for encontrada, mais nenhum atributo correspondente será avaliado.
- **Aplicar esse mapeamento**
    - **Sempre** – aplicar esse mapeamento nas ações de criação e atualização do usuário
    - **Somente durante a criação** – aplicar esse mapeamento somente nas ações de criação de usuário


## <a name="what-you-should-know"></a>O que você deve saber

O Microsoft Azure AD fornece uma implementação muito eficiente de um processo de sincronização. Em um ambiente inicializado, apenas os objetos que precisam de atualização são processados durante um ciclo de sincronização. Atualizar mapeamentos de atributo tem um impacto no desempenho de saudação de um ciclo de sincronização. Uma configuração de mapeamento de atributo de toohello de atualização requer que todos os toobe de objetos gerenciados reavaliadas. É um melhor prática tookeep Olá número recomendado de mapeamentos de atributo tooyour alterações consecutivas no mínimo.

## <a name="next-steps"></a>Próximas etapas

* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md)
* [Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de escopo para provisionamento de usuários](active-directory-saas-scoping-filters.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)
* [Notificações de provisionamento de conta](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

