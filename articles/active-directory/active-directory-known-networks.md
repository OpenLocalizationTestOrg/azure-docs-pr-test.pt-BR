---
title: "Redes aaaKnown Olá portal clássico do Azure | Microsoft Docs"
description: "Configurando redes conhecidos, você pode evitar ter endereços IP que pertencem a sua organização incluída no hello entradas de várias regiões geográficas e entradas de endereços IP com relatórios de atividade suspeita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Redes conhecidas

> [!div class="op_single_selector"]
> * [Portal clássico do Azure](active-directory-known-networks.md)
> * [Portal do Azure](active-directory-known-networks-azure-portal.md)
> 
> 


Você pode usar o acesso do Azure Active Directory e uso relatórios toogain visibilidade Olá integridade e segurança do diretório da sua organização. Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.

É possível que o hello "*entradas de várias regiões geográficas*"e"*entradas de endereços IP com atividade suspeita*" relatórios incorretamente sinalizador endereços IP que são realmente pertencentes a sua organização. 

Por exemplo, isso pode ocorrer quando: 

* Um usuário em seu escritório Boston entrou remotamente tooyour data center em são Francisco gatilhos Olá relatório de "Entradas de várias regiões geográficas" 
* Um usuário de sua organização tenta toosign em várias vezes com uma saudação de gatilhos de senha incorreta relatório de "Entradas de endereços IP com atividade suspeita" 

tooprevent nesses casos de segurança enganosa gerando relatórios, você deve adicionar conhecidos intervalos toohello lista de endereços IP do endereço IP público de sua organização.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>intervalos de endereço IP público de sua organização tooadd, execute Olá etapas a seguir:

1. Logon toohello [portal de gerenciamento do Azure](https://manage.windowsazure.com).

2. No painel esquerdo do hello, clique em **do Active Directory**. 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. Em Olá **diretório** , selecione seu diretório.

4. No menu de saudação na parte superior de saudação, clique em **configurar**. 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. Na guia Configurar de hello, vá muito**seus intervalos de endereços IP públicos organizações** 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. Clique em **Adicionar Intervalos de Endereços IP conhecidos**.

7. Adicione seus intervalos de endereços na caixa de diálogo de saudação que aparece e, em seguida, clique botão de seleção de hello quando você terminar. 

    ![Redes conhecidas](./media/active-directory-known-networks/known-netwoks-04.png)

**Recursos adicionais:**

* [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md)
* [Entradas de endereços IP com atividade suspeita](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Entradas de várias regiões geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md)

