---
title: "aaaProperties de um usuário de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "As propriedades do usuário de colaboração B2B do Azure Active Directory podem ser configuradas"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Propriedades de um usuário de colaboração B2B do Azure Active Directory

Um usuário de colaboração entre empresas (B2B) do Azure Active Directory (AD do Azure) é um usuário com UserType = Convidado. Este usuário convidado normalmente é de uma organização de parceiro e limitou os privilégios em hello para enviar o convite de diretório, por padrão.

Dependendo da saudação convidar as necessidades da organização, um usuário de colaboração B2B do Azure AD pode ser em uma saudação conta estados a seguir:

- Estado 1: Hospedada em uma instância externa do AD do Azure e representado como um usuário convidado em Olá convidar organização. Nesse caso, Olá B2B usuário entrar usando uma conta do AD do Azure que pertence o locatário toohello convidado. Se a organização do parceiro de saudação não usa o AD do Azure, o usuário convidado saudação do AD do Azure ainda é criado. requisitos de saudação são que eles resgatar seu convite e AD do Azure verifica seu endereço de email. Essa disposição também é chamada de locação JIT (just-in-time) ou, às vezes, de locação "viral".

- Estado 2: Hospedada em uma conta da Microsoft e representado como um usuário convidado na organização do host de saudação. Nesse caso, o usuário convidado de saudação entra com uma conta da Microsoft. Olá convidado social a identidade de usuário (google.com ou semelhante), que não é uma conta da Microsoft, é criado como uma conta da Microsoft durante o resgate de oferta.

- Estado 3: Hospedada no local Active Directory da organização do host Olá e sincronizados com o Azure da organização do host Olá AD. Durante esta versão, você deve usar o PowerShell toomanually alteração Olá UserType desses usuários na nuvem de saudação.

- Estado 4: Adaptadores de rede na Azure do organização do host AD com UserType = convidado e credenciais Olá host organização gerencia.

  ![Exibindo iniciais do emissor do convite Olá](media/active-directory-b2b-user-properties/redemption-diagram.png)


Agora, vamos ver a aparência de um usuário de colaboração B2B do AD do Azure no Estado 1 no Azure AD.

### <a name="before-invitation-redemption"></a>antes do resgate do convite

![Antes do resgate de oferta](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>após o resgate do convite

![Depois do resgate de oferta](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Propriedades de chave de usuário de colaboração de saudação do Azure AD B2B
### <a name="usertype"></a>UserType
Essa propriedade indica a relação de saudação de aluguel de host Olá usuário toohello. Essa propriedade pode assumir dois valores:
- Membro: Este valor indica um funcionário da empresa de host hello e um usuário na folha de pagamento da organização hello. Por exemplo, este usuário espera toohave acessar somente toointernal sites. Esse usuário não seria considerado um colaborador externo.

- Convidado: Este valor indica um usuário que não é considerado empresa toohello interno, como um parceiro externo, parceiro, cliente ou usuário semelhante. Esse usuário não ser esperado tooreceive memorando interno do CEO ou receber benefícios da empresa, por exemplo.

  > [!NOTE]
  > Olá UserType não tem nenhuma relação toohow Olá usuário se autentica no, a função de diretório de saudação do usuário Olá e assim por diante. Essa propriedade simplesmente indica Olá relação toohello host organização e permite que a organização Olá tooenforce políticas que dependem desta propriedade.

### <a name="source"></a>Fonte
Essa propriedade indica como o usuário Olá entrar.

- Usuário convidado: esse usuário foi convidado, mas ainda não resgatou seu convite.

- Externa do Active Directory: Este usuário está hospedado em uma organização externa e autentica por meio de uma conta do AD do Azure que pertence a toohello outra organização. Esse tipo de entrada corresponde tooState 1.

- Conta da Microsoft: este usuário está hospedado em uma conta da Microsoft e é autenticado usando uma conta da Microsoft. Esse tipo de entrada corresponde tooState 2.

- Windows Server Active Directory: Este usuário está conectado do Active Directory do local que pertence a organização toothis. Esse tipo de entrada corresponde tooState 3.

- Active Directory do Azure: Esse usuário é autenticado usando uma conta do AD do Azure que pertence a organização toothis. Esse tipo de entrada corresponde tooState 4.
  > [!NOTE]
  > A origem e o UserType são propriedades independentes. O valor de origem não envolve um valor específico para o UserType.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Os usuários B2B do AD do Azure podem ser adicionados como membros em vez de convidados?
Normalmente, um usuário B2B do Azure AD e o usuário convidado são sinônimos. Portanto, um usuário de colaboração B2B do AD do Azure é adicionado por padrão como um usuário com UserType = Convidado. No entanto, em alguns casos, a organização do parceiro de saudação é que um membro de uma organização de host Olá maior organização toowhich também pertence. Nesse caso, a organização de host Olá seja tootreat usuários na organização do parceiro de saudação como membros em vez de convidados. Use Olá APIs do Azure AD B2B convite Manager tooadd ou convidar um usuário da organização do hello parceiro organização toohello host como um membro.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filtro para usuários convidados no diretório Olá

![Como filtrar usuários convidados](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Converter UserType
Atualmente, é possível que os usuários tooconvert UserType do membro tooGuest e vice-versa usando o PowerShell. No entanto, Olá propriedade UserType deve toorepresent Olá relação toohello organização. Portanto, o valor dessa propriedade Olá deve alterar somente se a relação de saudação de organização de toohello saudação do usuário altera. Se a relação de saudação do usuário Olá mudar, deve, como se Olá UPN (UPN) deve ser alterada, abordados? Usuário Olá continue toohave acesso toohello mesmos recursos? Uma caixa de correio deve ser atribuída? Portanto, é recomendável não alterar Olá UserType usando o PowerShell como uma atividade atômica. Além disso, caso essa propriedade se torne imutável usando o PowerShell, é melhor não assumir uma dependência desse valor.

## <a name="remove-guest-user-limitations"></a>Como remover limitações do usuário convidado
Pode haver casos em que você deseja toogive seus privilégios mais altos de usuários do convidado. Você pode adicionar uma função de tooany de usuário convidado e até mesmo remover restrições ao usuário convidado saudação padrão em Olá diretório toogive uma saudação do usuário mesmo privilégios como membros.

É possível tooturn off limitações de usuário de convidado saudação padrão para que um usuário convidado no diretório de empresa Olá receber Olá as mesmas permissões que um usuário do membro.

![Como remover limitações do usuário convidado](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Auditoria e relatórios de um usuário de colaboração B2B](active-directory-b2b-auditing-and-reporting.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
