---
title: "aaaTroubleshooting a associação dinâmica de grupos | Microsoft Docs"
description: "Solução de problemas para a associação dinâmica para grupos no Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Solucionando problemas de associações dinâmicas a grupos
**Configurei uma regra em um grupo, mas nenhuma associação foi atualizada no grupo de saudação**<br/>Verifique se esse Olá **Habilitar gerenciamento de grupo de delegado** configuração está definida muito**Sim** em Olá **configurar** guia. Você verá essa configuração somente se você estiver conectado como um toowhom usuário uma licença Azure Active Directory Premium é atribuído. Verifique Olá valores para atributos de usuário na regra Olá: há usuários que atendem Olá regra?

**Configurei uma regra, mas agora os membros existentes de saudação da regra de saudação são removidos**<br/>Este comportamento é esperado. Membros existentes do grupo de saudação são removidos quando uma regra é habilitada ou alterada. os usuários de saudação retornados da avaliação de regra de saudação são adicionados como grupo de toohello de membros.     

**Não vejo as alterações da associação instantaneamente quando adiciono ou altero uma regra, por que não?**<br/>A avaliação de associação dedicada é feita periodicamente em um processo assíncrono em segundo plano. Quanto tempo Olá processo usa é determinado pelo número de saudação de usuários em seu diretório e Olá o tamanho de grupo Olá criado como resultado de regra de saudação. Normalmente, os diretórios com um número pequeno de usuários verá alterações de associação de grupo de saudação em menos de alguns minutos. Diretórios com um grande número de usuários podem levar 30 minutos ou mais toopopulate.

### <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
