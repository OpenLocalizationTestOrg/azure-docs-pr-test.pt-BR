---
title: "aaaCharacteristics do Active Directory do Azure locatário intercaction | Microsoft Docs"
description: "Gerenciar os locatários do Azure Active Directory considerando os locatários como recursos totalmente independentes"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Entender como interagem vários locatários do Azure Active Directory

No Azure Active Directory (AD do Azure), cada locatário é um recurso completamente independente: Olá de um ponto logicamente independente de outros locatários que você gerencia. Não há nenhuma relação pai-filho entre locatários. Essa independência entre locatários inclui independência de recursos, independência administrativa e independência de sincronização.

## <a name="resource-independence"></a>Independência de recursos
* Se você cria ou excluir um recurso em um locatário, ela não tem efeito sobre qualquer recurso em outro locatário, com exceção de saudação parcial de usuários externos. 
* Se você usar um de seus nomes de domínio com um locatário, ele não poderá ser usado com nenhum outro locatário.

## <a name="administrative-independence"></a>Independência administrativa
Se um usuário não administrativo do locatário “Contoso” criar um locatário de teste “Teste”:

* Por padrão, o usuário de saudação que cria um locatário é adicionado como um usuário externo nessa novo locatário e função de administrador global Olá atribuído no locatário.
* os administradores de saudação do locatário 'Contoso' têm tootenant sem privilégios administrativos diretos 'Test', a menos que um administrador de "Teste" especificamente conceda a eles esses privilégios. No entanto, os administradores de 'Contoso' podem controlar o acesso tootenant 'Test' se controle de conta de usuário Olá criado 'Test'.
* Se você adicionar ou remover uma função de administrador para um usuário em um locatário, o alteração Olá fará não afetam funções de administrador de saudação que Olá usuário tem em outro locatário.

## <a name="synchronization-independence"></a>Independência de sincronização
Você pode configurar cada Azure independentemente do AD locatário tooget dados sincronizados a partir de uma única instância do:

* ferramenta de Connect Olá AD do Azure, toosynchronize dados com uma única floresta do AD.
* Olá locatário do Azure Active conector para o Forefront Identity Manager, toosynchronize dados com um ou mais locais florestas e/ou fontes de dados de AD do Azure não.

## <a name="add-an-azure-ad-tenant"></a>Adicionar um locatário do Azure AD
tooadd um locatário Azure AD em Olá portal do Azure, entrar muito[Olá portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do AD do Azure e, Olá esquerda, selecione **novo**.

> [!NOTE]
> Ao contrário de outros recursos do Azure, os locatários não são recursos filho de uma assinatura do Azure. Se sua assinatura do Azure é cancelada ou expirada, você ainda pode acessar os dados de locatário usando o PowerShell do Azure, hello Azure Graph API ou Olá Office 365 Admin Center. Você também pode associar outra assinatura locatário hello.
>

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral ampla dos problemas de licenciamento e as melhores práticas do Azure AD, consulte [O que é o licenciamento de locatário do Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
