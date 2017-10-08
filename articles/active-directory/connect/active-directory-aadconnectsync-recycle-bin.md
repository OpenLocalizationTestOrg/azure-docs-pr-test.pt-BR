---
title: "Sincronização do Azure AD Connect: habilitar a lixeira do AD | Microsoft Docs"
description: "Este tópico recomenda o uso de saudação do recurso Lixeira do AD do Azure AD Connect."
services: active-directory
keywords: "Lixeira do AD, exclusão acidental, âncora de origem"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Sincronização do Azure AD Connect: habilitar a lixeira do AD
É recomendável que você habilite o recurso de Lixeira Olá AD para seus diretórios Active local, que são sincronizado tooAzure AD. 

Se você excluiu acidentalmente um local o objeto de usuário do AD e restauração-o usando o recurso de hello, AD do Azure restaura o objeto de usuário do AD do Azure correspondente hello.  Para obter informações sobre o recurso de Lixeira Olá AD, consulte tooarticle [visão geral do cenário de restauração de excluir objetos do Active Directory](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Benefícios da habilitação Olá AD Lixeira
Esse recurso ajuda a restaurar objetos de usuário do AD do Azure fazendo Olá seguinte:

* Se você excluiu acidentalmente um local em objeto de usuário do AD, objeto de usuário do AD do Azure correspondente Olá será excluído no hello próximo ciclo de sincronização. Por padrão, o AD do Azure mantém objeto de usuário do AD do Azure Olá excluído no estado excluído por 30 dias.

* Se você tiver local recurso Lixeira do AD habilitado, você pode restaurar Olá excluído local objeto de usuário do AD sem alterar seu valor de âncora de origem. Quando a saudação recuperados no local o objeto de usuário do AD está sincronizado tooAzure AD, Azure AD irá restaurar Olá correspondente excluído o objeto de usuário do AD do Azure. Para obter informações sobre o atributo de âncora de origem, consulte tooarticle [do Azure AD Connect: conceitos de projeto](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Se você não tiver local AD reciclar o recurso de compartimento habilitado, talvez seja necessário toocreate um objeto AD usuário objeto tooreplace Olá excluído. Se serviço de sincronização do Azure AD Connect é configurado toouse gerada pelo sistema AD atributo (como o ObjectGuid) para o atributo de âncora de origem hello, hello recém-criado objeto de usuário do AD será não têm Olá mesmo valor de âncora de origem como Olá excluiu o objeto de usuário do AD. Quando hello recém-criado objeto de usuário do AD está sincronizada tooAzure AD, o AD do Azure cria um novo objeto de usuário do AD do Azure em vez de restaurar o objeto de usuário do AD do Azure Olá excluídos por software.

> [!NOTE]
> Por padrão, o Azure AD mantém objetos de usuário excluídos do Azure AD em estado de exclusão temporária durante 30 dias antes que eles sejam excluídos permanentemente. No entanto, os administradores podem acelerar exclusão Olá desses objetos. Depois que os objetos de saudação são excluídos permanentemente, não podem ser recuperados, mesmo se a Lixeira do AD está ativado no local.



## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)

* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
