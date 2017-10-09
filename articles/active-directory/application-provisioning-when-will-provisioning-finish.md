---
title: "aaaUser Provisionando o aplicativo de galeria tooan AD do Azure está levando horas ou mais | Microsoft Docs"
description: Como toofind out por que o provisionamento de aplicativo tooyour pode estar demorando mais tempo do que esperado
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>Provisionamento de aplicativo da Galeria de tooan AD do Azure do usuário está levando horas ou mais

Quando é preciso habilitar o provisionamento automático para um aplicativo, a sincronização inicial Olá pode levar de horas de tooseveral de 20 minutos, dependendo do tamanho de Olá Olá diretório AD do Azure e o número de saudação de usuários em escopo para provisionamento. 

As sincronizações subsequentes após a sincronização inicial Olá ser mais rápido, Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial hello, melhorando o desempenho de sincronizações subsequentes.

## <a name="how-tooimprove-provisioning-performance"></a>Como tooimprove provisionamento de desempenho

Se a sincronização inicial hello está demorando mais do que algumas horas, há algo que você pode fazer tooimprove desempenho:

-   **Filtros de escopo de usuário.** Filtros de escopo permitem toofine ajustar dados de Olá Olá extrai provisionamento de serviço do AD do Azure, filtrando usuários com base em valores de atributo específicos. Para obter mais informações sobre filtros de escopo, consulte [provisionamento de aplicativos com base em atributo com filtros de escopo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

## <a name="next-steps"></a>Próximas etapas
[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md)

