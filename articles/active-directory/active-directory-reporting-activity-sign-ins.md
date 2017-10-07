---
title: "relatórios de atividade aaaSign no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Relatórios de atividade toosign de Introdução no portal do Azure Active Directory Olá"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Relatórios de atividade de entrada no portal do Azure Active Directory Olá

Com o Azure Active Directory (AD do Azure) reporting em Olá [portal do Azure](https://portal.azure.com), você pode obter informações de saudação necessário toodetermine como seu ambiente está fazendo.

Olá arquitetura de relatórios no Active Directory do Azure consiste em Olá componentes a seguir:

- **Atividade** 
    - **Atividades de entrada** – informações sobre o uso de saudação de aplicativos gerenciados e atividades de entrada do usuário
    - **Logs de auditoria** – informações de atividade do sistema sobre o gerenciamento de usuários e de grupos, sobre os aplicativos gerenciados e sobre as atividades de diretório.
- **Segurança** 
    - **Entradas arriscadas** -uma entrada arriscado é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é proprietário legítimo Olá uma conta de usuário. Para obter mais detalhes, veja Entradas de risco.
    - **Usuários sinalizados para riscos** - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida. Para obter mais detalhes, consulte Usuários sinalizados para risco.

Este tópico fornece uma visão geral das atividades de entrada hello.

## <a name="pre-requisite"></a>Pré-requisito

### <a name="who-can-access-hello-data"></a>Quem pode acessar dados Olá?
* Usuários na função de administrador de segurança ou segurança leitor Olá
* Administradores globais
* Qualquer usuário (não administradores) pode acessar suas próprias entradas 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Qual licença do AD do Azure precisa de atividade de entrada tooaccess?
* Seu locatário deve ter uma licença Azure AD Premium associada a ele toosee Olá tudo sign-relatório de atividade


## <a name="signs-in-activities"></a>Atividades de entrada

Com informações de saudação fornecidas pelo relatório de entrada do usuário de saudação, você encontrar respostas tooquestions como:

* O que é Olá entrar padrão de um usuário?
* Quantos usuários entraram em uma semana?
* Qual é o status de saudação destas entradas?

Seu primeiro entrada tooall de ponto de entrada atividades dados **entradas** na seção de atividade de saudação do **Azure Active**.


![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/61.png "Atividade de entrada")


Um log de auditoria tem um modo de exibição de lista padrão que mostra:

- usuário relacionado Olá
- Olá aplicativo hello tenha assinado do usuário para
- status de entrada Hello
- hora de entrada Hello

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")

Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/19.png "Atividade de entrada")

Isso permite que os campos adicionais toodisplay ou remover campos que já estão sendo exibidos.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/42.png "Atividade de entrada")

Ao clicar em um item na exibição de lista Olá, você deve obter todos os detalhes disponíveis sobre ele.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/43.png "Atividade de entrada")


## <a name="filtering-sign-in-activities"></a>Filtragem de atividades de entrada

toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar dados de entradas de saudação usando Olá campos a seguir:

- Intervalo de tempo
- Usuário
- Aplicativo
- Cliente
- Status de entrada

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/44.png "Atividade de entrada")


Olá **intervalo de tempo** filtro habilita tooyou toodefine um período de tempo para Olá retornou dados.  
Os valores possíveis são:

- 1 mês
- 7 dias
- 24 horas
- Personalizado

Quando você seleciona um período de tempo personalizado, pode configurar uma hora de início e uma hora de término.

Olá **usuário** filtro permite que nome de saudação toospecify ou Olá principal nome de usuário (UPN) do usuário Olá importantes para você.

Olá **aplicativo** filtro permite toospecify nome de saudação do aplicativo hello importantes para você.

Olá **cliente** filtro permite que você toospecify informações sobre o dispositivo Olá importantes para você.

Olá **status de entrada** filtro permite tooselect de saudação filtro a seguir:

- Todos
- Sucesso
- Failure


## <a name="sign-in-activities-shortcuts"></a>Atalhos de atividades de entrada

Além disso tooAzure do Active Directory, Olá portal do Azure oferece dois dados de toosign em atividades de pontos de entrada adicional:

- Usuários e grupos
- Aplicativos empresariais


### <a name="users-and-groups-sign-ins-activities"></a>Atividades de entrada de usuários e grupos

Com informações de saudação fornecidas pelo relatório de entrada do usuário de saudação, você encontrar respostas tooquestions como:

- O que é Olá entrar padrão de um usuário?
- Quantos usuários entraram em uma semana?
- Qual é o status de saudação destas entradas?



Os dados de toothis de ponto de entrada são Olá usuário entrar no gráfico de saudação **visão geral** seção em **usuários e grupos**.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/45.png "Atividade de entrada")

Olá usuário entrar gráfico mostra agregações semanais do sinal ins para todos os usuários em um determinado período de tempo. padrão de saudação para Olá o período de tempo é 30 dias.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/46.png "Atividade de entrada")

Quando você clica em um dia no gráfico de entrada hello, você obtém uma lista detalhada das atividades de entrada hello para esse dia.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/41.png "Atividade de entrada")

Cada linha na permite de lista de atividades de entrada hello que Olá informações detalhadas sobre Olá selecionado entrar como:

* Quem entrou?
* O que foi Olá relacionadas UPN?
* Qual aplicativo era o destino de saudação de saudação entrar?
* O que é o endereço IP de saudação do hello entrar?
* Qual era o status de saudação do hello entrar?

Olá **entradas** opção fornece uma visão geral completa de todas as entradas do usuário.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/51.png "Atividade de entrada")



## <a name="usage-of-managed-applications"></a>Uso de aplicativos gerenciados

Com uma exibição centrada no aplicativo de seus dados de entrada, você pode responder a perguntas como:

* Quem está usando meus aplicativos?
* Quais são os principais 3 aplicativos Olá em sua organização?
* Recentemente, eu implantei um aplicativo. Como ele está se saindo?

Os dados de toothis de ponto de entrada são maiores 3 aplicativos Olá em sua organização no último relatório de 30 dias Olá no hello **visão geral** seção em **aplicativos empresariais**.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/64.png "Atividade de entrada")

Olá aplicativo uso gráfico semanal agregações de entradas para seus aplicativos de 3 principais em um determinado período de tempo. padrão de saudação para Olá o período de tempo é 30 dias.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/47.png "Atividade de entrada")

Se desejar, você pode definir o foco de saudação em um aplicativo específico.


![Relatórios](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Relatórios")

Quando você clica em um dia no gráfico de uso do aplicativo hello, você pode obter uma lista detalhada das atividades de entrada hello.


![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/48.png "Atividade de entrada")


Olá **entradas** opção fornece uma visão geral completa de todos os aplicativos de tooyour de eventos de entrada.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins/49.png "Atividade de entrada")



## <a name="next-steps"></a>Próximas etapas

Se você quiser tooknow mais informações sobre códigos de erro de atividade de entrada, consulte Olá [entrar códigos de erro do atividade relatórios no portal do Azure Active Directory Olá](active-directory-reporting-activity-sign-ins-errors.md).

