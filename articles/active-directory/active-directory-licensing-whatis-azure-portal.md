---
title: "aaaWhat é licenciamento no Azure Active Directory baseado em grupo? | Microsoft Docs"
description: "Descrição de licenciamento baseado em grupo do Azure Active Directory, como ele funciona e práticas recomendadas"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Noções básicas de licenciamento baseado em grupo no Azure Active Directory

O uso de serviços de nuvem pagos da Microsoft, como Office 365, Enterprise Mobility + Security, Dynamics CRM e outros produtos similares, exige licenças. Essas licenças são atribuídas usuário tooeach que precisa de acesso toothese serviços. os administradores de licenças toomanage, usam um dos portais de gerenciamento da saudação (Office ou do Azure) e cmdlets do PowerShell. Azure Active Directory (AD do Azure) é infraestrutura subjacente de saudação que dá suporte ao gerenciamento de identidade para todos os serviços de nuvem da Microsoft. O Azure AD armazena informações sobre estados de atribuição de licença para usuários.

Até agora, licenças podem ser atribuídas apenas no nível de usuário individual hello, que pode dificultar o gerenciamento em larga escala. Por exemplo, tooadd ou remover licenças de usuário com base em alterações organizacionais, como usuários ingressar ou sair Olá organização ou um departamento, um administrador geralmente deve gravar um script do PowerShell complexas. Esse script faz chamadas individuais toohello serviço de nuvem.

tooaddress os desafios, o AD do Azure agora inclui o licenciamento baseado em grupo. Você pode atribuir um ou mais grupo de tooa de licenças de produto. AD do Azure assegura que as licenças de saudação sejam atribuídas tooall membros do grupo de saudação. Quaisquer novos membros que ingressar Olá grupo recebem licenças apropriadas hello. Quando eles saem grupo hello, essas licenças são removidas. Isso elimina a necessidade de saudação para automatizar o gerenciamento de licenças por meio do PowerShell tooreflect alterações na estrutura departamental em uma base por usuário e organização de saudação.

## <a name="features"></a>Recursos

Aqui estão os principais recursos de saudação do licenciamento baseado em grupo:

- Licenças podem ser atribuídas tooany grupo de segurança no AD do Azure. Os grupos de segurança podem ser sincronizados localmente usando o Azure AD Connect. Você também pode criar grupos de segurança diretamente no AD do Azure (também chamados de grupos somente em nuvem), ou automaticamente por meio do recurso de grupo dinâmico Olá AD do Azure.

- Quando uma licença de produto é atribuída tooa grupo, o administrador de saudação pode desabilitar um ou mais planos de serviço no produto hello. Normalmente, isso é feito quando organização Olá ainda não está pronto toostart usando um serviço de um produto. Por exemplo, administrador Olá pode atribuir o departamento de tooa do Office 365, mas desabilitar temporariamente o serviço do Yammer hello.

- Todos os serviços de nuvem da Microsoft que exigem licenciamento no nível do usuário têm suporte. Isso inclui todos os produtos do Office 365, Enterprise Mobility + Security e Dynamics CRM.

- Licenciamento baseado em grupo está disponível atualmente apenas por meio de [Olá portal do Azure](https://portal.azure.com). Se você usar principalmente outros portais de gerenciamento para o gerenciamento de usuário e grupo, como o portal de saudação Office 365, você pode continuar toodo assim. Mas você deve usar licenças do hello toomanage portal do Azure no nível do grupo.

- O Azure AD gerencia automaticamente as modificações de licença que resultam das alterações de associação de grupo. Normalmente, as modificações de licença entram em vigor dentro de minutos após uma alteração de associação.

- Um usuário pode ser membro de vários grupos com políticas de licença especificadas. Um usuário também pode ter algumas licenças que foram atribuídas diretamente, fora de todos os grupos. Olá resultante de estado do usuário é uma combinação de todos os produtos atribuídos e licenças de serviço.

- Em alguns casos, licenças não podem ser tooa usuário atribuídas. Por exemplo, talvez não haja licenças suficientes disponíveis no locatário hello, ou serviços conflitantes podem tiverem sido atribuídos em Olá mesmo tempo. Os administradores têm acesso tooinformation sobre quem AD do Azure não pôde totalmente processar licenças do grupo de usuários. Eles podem agir corretivamente com base nessas informações.

- Durante a visualização pública, uma assinatura de avaliação ou paga para edições do Azure AD Basic ou Premium é necessária no gerenciamento de licença baseada em grupo Olá locatário toouse.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre outros cenários de gerenciamento de licenças por meio de licenciamento baseado em grupo, consulte:

* [Introdução às licenças do Azure Active Directory](active-directory-licensing-get-started-azure-portal.md)
* [Atribuir licenças tooa grupo no Active Directory do Azure](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificar e resolver problemas de licença para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Como indivíduo toomigrate licenciado usuários licenciamento no Azure Active Directory com base em toogroup](active-directory-licensing-group-migration-azure-portal.md)
* [Cenários adicionais de licenciamento baseado em grupo do Azure Active Directory](active-directory-licensing-group-advanced.md)
