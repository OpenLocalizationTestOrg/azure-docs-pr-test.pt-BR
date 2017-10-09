---
title: locais de aaaNamed no Active Directory do Azure | Microsoft Docs
description: "Configurando denominado locais, você poderá evitar IP endereços pertencentes a sua organização geram falsos positivos para locais de tooatypical viagem impossível Olá corre o risco de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Localizações nomeadas no Azure Active Directory

Com hello denominado recursos locais do Active Directory do Azure, você pode rotular intervalos de endereço IP confiável em sua organização. Em seu ambiente, você pode usar locais nomeadas no contexto de saudação da detecção de saudação do [eventos de risco](active-directory-reporting-risk-events.md). recurso de saudação ajuda a reduzir o número de saudação de relatado falsos positivos para Olá *viagem impossível tooatypical locais* corre o risco de tipo de evento. 

## <a name="configuration"></a>Configuração

tooconfigure um local nomeado:

1. Entrar toohello [portal do Azure](https://portal.azure.com) como administrador global.

2. No painel esquerdo do hello, clique em **Active Directory do Azure**.

    ![link do Active Directory do Azure Olá no painel esquerdo da saudação](./media/active-directory-named-locations/01.png)

3. Em Olá **Active Directory do Azure** folha em Olá **segurança** seção, clique em **acesso condicional**.

    ![Olá comando de acesso condicional](./media/active-directory-named-locations/05.png)


4. Em Olá **acesso condicional** folha em Olá **gerenciar** seção, clique em **chamado locais**.

    ![Olá nomeados locais comando](./media/active-directory-named-locations/06.png)


5. Em Olá **chamado locais** folha, clique em **novo local**.

    ![Olá novo comando de local](./media/active-directory-named-locations/07.png)


6. Em Olá **novo** folha, Olá a seguir:

    ![blade de nova Olá](./media/active-directory-named-locations/08.png)

    a. Em Olá **nome** , digite um nome para seu local nomeada.

    b. Em Olá **intervalos IP** , digite um intervalo de IP. intervalo IP Hello precisa toobe em Olá *CIDR* formato (CIDR).  

    c. Clique em **Criar**.



## <a name="what-you-should-know"></a>O que você deve saber

**Atualizações em massa**: quando você cria ou atualiza locais nomeadas, as atualizações em massa, você pode carregar ou baixar um arquivo CSV com os intervalos IP hello. Um carregamento adiciona intervalos IP hello na lista de toohello Olá arquivos em vez de substituir a lista de saudação.

![Olá Upload e Download de links](./media/active-directory-named-locations/09.png)


**Limitações**: você pode definir um máximo de 60 locais nomeados, com um tooeach de intervalo atribuído IP deles. Se você tiver apenas um local nomeado configurado, você pode definir intervalos IP too500 para ele.


## <a name="next-steps"></a>Próximas etapas

toolearn mais informações sobre eventos de risco, consulte [eventos de risco do Active Directory do Azure](active-directory-reporting-risk-events.md).

