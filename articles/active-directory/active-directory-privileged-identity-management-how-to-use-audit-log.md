---
title: "log de auditoria de saudação do aaaHow toouse no Azure AD Privileged Identity Management | Microsoft Docs"
description: "Saiba como log de auditoria de saudação de toouse na extensão do hello Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Usando o log de auditoria Olá PIM
Você pode usar toosee de log de auditoria de gerenciamento de identidade com privilégios (PIM) Olá todas as atribuições de saudação do usuário e ativações dentro de um determinado período de tempo. Se você quiser toosee histórico de auditoria completa Olá da atividade em seu locatário, incluindo o administrador, o usuário final e a atividade de sincronização, você pode usar o hello [relatórios de acesso e uso do Active Directory do Azure.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Navegue toohello log de auditoria
De saudação [portal do Azure](https://portal.azure.com) dashboard, selecione Olá **do Azure AD Privileged Identity Management** aplicativo. A partir daí, acessar o log de auditoria Olá clicando **gerenciar funções privilegiadas** > **histórico de auditoria** no painel PIM hello.

## <a name="hello-audit-log-graph"></a>gráfico de log de auditoria de saudação
Você pode usar o hello audit log tooview Olá total de ativações, ativações máx por dia e ativações médias por dia em um gráfico de linha.  Você também pode filtrar dados saudação pela função se houver mais de uma função no histórico de auditoria de saudação.

Saudação de uso **tempo**, **ação**, e **função** botões toosort Olá log.

## <a name="hello-audit-log-list"></a>lista de log de auditoria de saudação
Olá colunas na lista de log de auditoria de saudação são:

* **Solicitante** -usuário Olá que solicitou a ativação da função hello ou alterar.  Se o valor de saudação é "Azure sistema", verifique o log de auditoria do Azure de saudação para obter mais informações.
* **Usuário** -usuário Olá que está sendo ativado ou tooa função atribuída.
* **Função** -função hello atribuídos ou ativado pelo usuário hello.
* **Ação** - ações de saudação solicitante hello. Isso pode incluir a atribuição, o cancelamento da atribuição, a ativação ou a desativação.
* **Tempo** - quando a ação de saudação ocorreu.
* **Raciocínio** -se que qualquer texto foi inserido no campo de razão de saudação durante a ativação, ele aparecerá aqui.
* **Expiração** : relevante apenas para a ativação de funções.

## <a name="filter-hello-audit-log"></a>Log de auditoria de saudação do filtro
Você pode filtrar as informações de saudação que aparece no log de auditoria Olá clicando Olá **filtro** botão.  Olá **folha de parâmetros de gráfico de atualização** será exibida.

Depois de definir filtros de saudação, clique em **atualização** dados de saudação toofilter no log de saudação.  Se dados saudação não aparecem imediatamente, atualize a página de saudação.

### <a name="change-hello-date-range"></a>Alterar o intervalo de datas Olá
Saudação de uso **hoje**, **semana passada**, **último mês**, ou **personalizado** botões toochange intervalo de tempo de saudação do log de auditoria de saudação.

Quando você escolhe Olá **personalizado** botão, você terá um **de** campo de data e um **para** toospecify campo um intervalo de datas para o log de saudação de data.  Você pode inserir datas de saudação no formato DD/MM/AAAA ou clique em Olá **calendário** ícone e escolha a data de saudação de um calendário.

### <a name="change-hello-roles-included-in-hello-log"></a>Alterar funções hello incluídas no log de saudação
Marque ou desmarque Olá **função** caixa de seleção próxima tooeach função tooinclude ou exclusão de saudação de log.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

