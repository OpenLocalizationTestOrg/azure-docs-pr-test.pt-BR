---
title: "relatórios de atividade de aaaAudit no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Relatórios de atividade no portal do Azure Active Directory Olá de auditoria toohello de Introdução"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Relatórios de atividade no portal do Azure Active Directory Olá de auditoria 

Com o relatório no Azure Active Directory (AD do Azure), você pode obter informações de saudação necessário toodetermine como seu ambiente está fazendo.

Olá arquitetura de relatórios no AD do Azure consiste em Olá componentes a seguir:

- **Atividade** 
    - **Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário
    - **Logs de auditoria** – informações de atividade do sistema sobre o gerenciamento de usuários e de grupos, sobre os aplicativos gerenciados e sobre as atividades de diretório.
- **Segurança** 
    - **Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário. Para obter mais detalhes, veja Entradas de risco.
    - **Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida. Para obter mais detalhes, consulte Usuários sinalizados para risco.

Este tópico fornece uma visão geral das atividades de auditoria de saudação.
 
## <a name="who-can-access-hello-data"></a>Quem pode acessar dados Olá?
* Usuários na função de administrador de segurança ou segurança leitor Olá
* Administradores globais
* Os usuários individuais (não administradores) podem ver suas próprias atividades


## <a name="audit-logs"></a>Logs de auditoria

logs de auditoria de saudação no Active Directory do Azure fornecem registros de atividades de sistema para fins de conformidade.  
É o primeiro tooall de ponto de entrada dados de auditoria **logs de auditoria** em Olá **atividade** seção **Active Directory do Azure**.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/61.png "Logs de auditoria")

Um log de auditoria tem um modo de exibição de lista padrão que mostra:

- Data de saudação e a hora da ocorrência da saudação
- Olá iniciador / ator (*que*) de uma atividade 
- Hello atividade (*que*) 
- destino de saudação

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/18.png "Logs de auditoria")

Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/19.png "Logs de auditoria")

Isso permite que os campos adicionais toodisplay ou remover campos que já estão sendo exibidos.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/21.png "Logs de auditoria")


Ao clicar em um item na exibição de lista Olá, você deve obter todos os detalhes disponíveis sobre ele.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/22.png "Logs de auditoria")


## <a name="filtering-audit-logs"></a>Filtragem de logs de auditoria

toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar os dados de auditoria hello usando Olá campos a seguir:

- Intervalo de datas
- Iniciado por (ator)
- Categoria
- Tipo de recurso de atividade
- Atividade

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/23.png "Logs de auditoria")


Olá **intervalo de datas** filtro habilita tooyou toodefine um período de tempo para Olá retornou dados.  
Os valores possíveis são:

- 1 mês
- 7 dias
- 24 horas
- Personalizado

Quando você seleciona um período de tempo personalizado, pode configurar uma hora de início e uma hora de término.

Olá **iniciada pelo** filtro permite que você toodefine nome de um ator ou seu nome de entidade de segurança universal (UPN).

Olá **categoria** filtro permite tooselect de saudação filtro a seguir:

- Todos
- Categoria principal
- Diretório principal
- Gerenciamento de senhas de autoatendimento
- Gerenciamento de grupo de autoatendimento
- Provisionamento de conta - Substituição de senha automática
- Usuários convidados
- Serviço MIM
- Identity Protection
- B2C

Olá **tipo de recurso de atividade** filtro permite tooselect Olá seguinte filtros:

- Todos 
- Agrupar
- Diretório
- Usuário
- Aplicativo
- Política
- Dispositivo
- outro

Quando você seleciona **grupo** como **tipo de recurso de atividade**, você obtém uma categoria de filtro adicional que permite que você tooalso fornecem uma **origem**:

- AD do Azure
- O365


Olá **atividade** filtro se baseia na categoria hello e seleção do tipo de recurso de atividade feitas. Você pode selecionar uma atividade específica que deseja toosee ou escolha todas as. 

Você pode obter a lista de saudação de todas as atividades de auditoria usando Olá Graph API https://graph.windows.net/$ atividades/tenantdomain/auditActivityTypes? api-version = beta, onde $tenantdomain = seu nome de domínio ou consulte o artigo toohello [relatório de auditoria eventos](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Atalhos de logs de auditoria

Além disso muito**Active Directory do Azure**, hello portal do Azure oferece dois pontos de entrada adicional tooaudit dados:

- Usuários e grupos
- Aplicativos empresariais

### <a name="users-and-groups-audit-logs"></a>Logs de auditoria de usuários e grupos

Com relatórios de auditoria com base em grupo e usuário, você pode obter respostas tooquestions como:

- Que tipos de atualizações foram usuários Olá aplicadas?

- Quantos usuários foram alterados?

- Quantas senhas foram alteradas?

- O que um administrador fez em um diretório?

- O que são grupos de saudação que foram adicionados?

- Existem grupos com alterações de associação?

- Os proprietários de saudação do grupo foram alterados?

- Quais licenças tiverem recebidas um usuário ou grupo tooa?

Se você quiser apenas tooreview dados toousers relacionados e grupos de auditoria, você pode encontrar uma exibição filtrada em **logs de auditoria** em Olá **atividade** seção Olá **usuários e grupos**. Esse ponto de entrada tem **Usuários e grupos** como **Tipo de Recurso de Atividade** pré-selecionado.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/93.png "Logs de auditoria")

### <a name="enterprise-applications-audit-logs"></a>Logs de auditoria de aplicativos empresariais

Com o aplicativo com base em relatórios de auditoria, você pode obter respostas tooquestions como:

* Quais são os aplicativos de saudação que foram adicionados ou atualizados?
* Quais são os aplicativos de saudação que foram removidos?
* Um princípio de serviço para um aplicativo foi alterado?
* Nomes de saudação de aplicativos foram alterados?
* Que forneceu o consentimento tooan aplicativo?

Se você quiser apenas tooreview dados de aplicativos tooyour relacionadas a auditoria, você pode encontrar uma exibição filtrada em **logs de auditoria** em Olá **atividade** seção Olá **aplicativos empresariais**  folha. Esse ponto de entrada tem **aplicativos empresariais** como **tipo de recurso de atividade** pré-selecionado.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/134.png "Logs de auditoria")

Você pode filtrar essa exibição para baixo toojust **grupos** ou apenas **usuários**.

![Logs de auditoria](./media/active-directory-reporting-activity-audit-logs/25.png "Logs de auditoria")


## <a name="next-steps"></a>Próximas etapas

Para obter uma visão geral de emissão de relatórios, consulte Olá [reporting do Active Directory do Azure](active-directory-reporting-azure-portal.md).

