---
title: "aaaUnlicensed relatório de uso | Microsoft Docs"
description: "Olá relatório de uso não licenciado paga de ajuda a que identificar os usuários não licenciados que estão usando recursos do AD do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Relatório de uso não licenciado
Olá relatório de uso não licenciado paga de ajuda a que identificar os usuários não licenciados que estão usando recursos do AD do Azure. Isso permite toomake melhor uso de licenças que você comprou e tooidentify você saber quando você pode precisar de mais licenças. 

relatório de saudação mostra o uso ativo de Olá recursos pago no hello últimos 30 dias. 

## <a name="report-structure"></a>Estrutura de relatório
| Nome da coluna | Descrição |
|:--- |:--- |
| Usuário Não Licenciado |Nome de usuário de saudação |
| Recurso |nome do recurso Hello. Por exemplo: acesso condicional |
| Aplicativo acessado |nome de saudação do aplicativo de saudação que está sendo acessado com recurso de saudação. Por exemplo: Office 365 SharePoint Online |

> [!NOTE]
> Se uma conta de usuário foi excluída Olá 'Não licenciado User' coluna será preenchida com uma ID, como 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Recurso de acesso condicional
Os usuários não licenciados serão sinalizados quando acessarem um serviço com a política de acesso condicional aplicada se não tiverem uma licença do Azure AD Premium. 

Isso se aplica a tooMFA / políticas de local, bem como dispositivo políticas que usar o Intune.

## <a name="see-also"></a>Consulte também
* [Usar o acesso condicional com o Office 365 e com outros aplicativos conectados ao Azure Active Directory](active-directory-conditional-access.md)
* [Introdução ao acesso condicional tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

