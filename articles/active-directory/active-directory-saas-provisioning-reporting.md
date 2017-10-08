---
title: "Relatórios sobre aplicativos tooSaaS de provisionamento de conta de usuário automático de Active Directory do Azure | Microsoft Docs"
description: "Saiba como toocheck Olá status de trabalhos de provisionamento de conta de usuário automático e tootroubleshoot Olá provisionamento de usuários individuais."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Tutorial: Relatórios sobre o provisionamento automático de conta de usuário


O Active Directory do Azure inclui um [conta de usuário do serviço de configuração](active-directory-saas-app-provisioning.md) que ajuda a automatizar Olá provisionamento desprovisionamento de contas de usuário em aplicativos SaaS e outros sistemas, para fins de saudação do ciclo de vida da identidade de ponta a ponta gerenciamento. AD do Azure suporta conectores para todos os aplicativos de saudação e sistemas em hello "Em destaque" seção de saudação de provisionamento do usuário pré-integrados [Galeria de aplicativos do AD do Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Este artigo descreve como o status de saudação toocheck de provisionamento de trabalhos depois que elas foram definidas e tootroubleshoot Olá provisionamento de usuários individuais e grupos.

## <a name="overview"></a>Visão geral

Provisionamento conectores são configurados principalmente e configurada usando Olá [portal de gerenciamento do Azure](https://portal.azure.com), pelos seguinte Olá [fornecido documentação](active-directory-saas-tutorial-list.md) para o aplicativo hello onde usuário provisionamento de conta é desejado. Depois de estarem configurados e em execução, os trabalhos de provisionamento para um aplicativo podem ser informados usando um dos dois métodos:

* **Portal de gerenciamento do Azure** -este artigo descreve principalmente ao recuperar informações de relatório da saudação [portal de gerenciamento do Azure](https://portal.azure.com), que fornece tanto um relatório de resumo de provisionamento, bem como provisionamento detalhadas logs para um determinado aplicativo de auditoria.

* **Audit API** -Active Directory do Azure também fornece uma API que permite a recuperação programática de saudação detalhadas provisionamento logs de auditoria de auditoria. Consulte [auditoria do Active Directory do Azure referência da API](active-directory-reporting-api-audit-reference.md) para toousing específicos da documentação essa API. Enquanto este artigo não aborda especificamente como toouse Olá API, ele detalhes sobre tipos de saudação do provisionamento de eventos que são registrados no log de auditoria de saudação.

### <a name="definitions"></a>Definições

Este artigo usa Olá seguintes termos, definidos abaixo:

* **Sistema de origem** -sincroniza o repositório de saudação de usuários que Olá serviço de provisionamento do AD do Azure do. Active Directory do Azure é o sistema de origem Olá para maioria de saudação do pré-integrado provisionamento conectores, no entanto, há algumas exceções (exemplo: a sincronização de entrada de dia de trabalho).

* **Sistema de destino** -sincroniza o repositório de saudação de usuários que Olá serviço de provisionamento do AD do Azure para. Isso normalmente é um aplicativo SaaS (exemplos: Salesforce, ServiceNow, Google Apps, Dropbox for Business), mas em alguns casos, pode ser um sistema local como o Active Directory (exemplo: a sincronização de entrada de dia de trabalho tooActive diretório).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Obtendo o provisionamento de relatórios do portal de gerenciamento do Azure Olá

tooget informações de relatório para um determinado aplicativo, o provisionamento inicial iniciando Olá [portal de gerenciamento do Azure](https://portal.azure.com) e toohello Enterprise aplicativo para o qual o provisionamento está configurado de navegação. Por exemplo, se estiver Provisionando usuários tooLinkedIn elevar, detalhes do aplicativo hello navegação caminho toohello é:

**Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos > LinkedIn Elevate**

A partir daqui, você pode acessar o relatório de resumo de provisionamento hello e logs de auditoria provisionamento hello, ambas descritas abaixo.


### <a name="provisioning-summary-report"></a>Relatório de resumo de provisionamento

Olá, relatório de resumo de provisionamento está visível no hello **provisionamento** guia para determinado aplicativo. Ele está localizado na seção de detalhes de sincronização Olá sob **configurações**e fornece Olá informações a seguir:

* Olá número total de usuários e grupos que tenham sido sincronizadas e estão no escopo para provisionamento entre sistemas de origem hello e Olá destino.

* última sincronização de saudação tempo Olá foi executada. As sincronizações normalmente ocorrem a cada 20 a 40 minutos, após uma sincronização ser concluída.

* Se uma sincronização completa inicial foi ou não concluída.

* Ou não Olá processo de provisionamento foi colocado em quarentena, e que motivo Olá para status de quarentena hello, por exemplo, é (toocommunicate falha com o sistema de destino devido a credenciais de administrador tooinvalid)

Olá, relatório de resumo de provisionamento deve ser Olá primeiro local de administradores aparência toocheck na integridade operacional de saudação do trabalho de provisionamento da saudação.

 ![Relatório resumido](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Logs de auditoria de provisionamento
Todas as atividades realizadas por Olá provisionamento de serviço são registradas nos logs de auditoria de saudação do AD do Azure, que podem ser exibidos em Olá **logs de auditoria** guia em Olá **provisionamento de conta** categoria. Alguns dos tipos de eventos de atividade incluídos no log são:

* **Importar eventos** -um evento de "importação" é registrado sempre que o serviço de provisionamento de saudação do AD do Azure recupera informações sobre um usuário individual ou grupo de um sistema de origem ou destino. Durante a sincronização, os usuários são recuperados do sistema de origem de saudação em primeiro lugar, com resultados Olá registrados como eventos de "importação". Olá as IDs de usuários Olá recuperado, em seguida, são consultadas contra Olá toocheck de sistema de destino caso existam, com resultados Olá também são registrados como eventos de "importação". Esses eventos registram todos os atributos de usuário mapeadas e os valores que foram vistos pelo serviço de provisionamento de saudação do AD do Azure em tempo de saudação do evento hello. 

* **Eventos de regra de sincronização** - esses eventos relatam os resultados de saudação de regras de mapeamento de atributo hello e qualquer configurado filtros de escopo, depois que os dados de usuário foi importados e avaliados de sistemas de origem e destino hello. Por exemplo, se um usuário em um sistema de origem é considerado toobe no escopo para provisionamento e considerado toonot existe no sistema de destino hello, este evento registra que Olá usuário será provisionado no sistema de destino de saudação. 

* **Exportar eventos** -um evento de "Exportar" é registrado sempre que o serviço de provisionamento de saudação do AD do Azure grava um usuário conta ou grupo de objeto tooa sistema de destino. Esses eventos registram todos os atributos de usuário e os valores que foram gravados pelo Olá serviço de provisionamento do AD do Azure em tempo de saudação do evento hello. Se houver um erro durante a gravação da saudação usuário conta ou grupo de objeto toohello sistema de destino, ele será exibido aqui.

* **Processar eventos de caução** -escrows processo ocorrem quando hello provisionamento serviço encontra uma falha durante a tentativa de uma operação e começa a operação de saudação tooretry em um intervalo de retirada de tempo. Um evento "caução" é registrado sempre que uma operação de provisionamento é desativada.

Ao examinar os eventos de provisionamento para um usuário individual, eventos de saudação normalmente ocorrem nesta ordem:

1. Evento de importação: usuário é recuperado do sistema de origem de saudação.

2. Evento de importação: o sistema de destino é consultado toocheck quanto à existência de saudação do usuário Olá recuperado.

3. Evento de regra de sincronização: dados do usuário de sistemas de origem e destino são avaliados em relação de atributo Olá configurado regras de mapeamento e toodetermine filtros de escopo de ação que, se houver, deve ser executada.

4. Exportar eventos: se o evento de regra de sincronização Olá determinado que uma ação deve ser executada (por exemplo, adicionar, atualizar, excluir), em seguida, os resultados de saudação de ação de saudação são registrados em um evento de exportação.

![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Como pesquisar eventos de provisionamento para um usuário específico

Olá, caso de uso mais comum para Olá provisionamento logs de auditoria é Olá toocheck status de uma conta de usuário individual de provisionamento. toolook eventos de provisionamento última Olá para um usuário específico:

1. Vá toohello **logs de auditoria** seção.

2. De saudação **categoria** menu, selecione **provisionamento de conta**.

3. Em Olá **intervalo de datas** menu, você deseja toosearch, de intervalo de datas Olá select

4. Em Olá **pesquisa** barra, insira a ID de usuário de saudação do usuário Olá desejar toosearch para. formato de saudação do valor de ID deve corresponder tudo o que você selecionou como Olá primário ID correspondente na configuração de mapeamento de atributo hello (por exemplo, userPrincipalName ou funcionário número de ID). valor de ID Olá necessário estarão visível na coluna de destino (s) de saudação.

5. Pressione Enter toosearch. Olá mais recente de provisionamento de eventos será retornado pela primeira vez.

6. Se os eventos são retornados, observe os tipos de atividade hello e se foram bem-sucedidas ou falharam. Se nenhum resultado for retornado, isso significa Olá usuário não existe, ou ainda não foi detectado pelo Olá processo de provisionamento se uma sincronização completa não tiver sido concluído.

7. Clique em eventos individuais tooview estendido detalhes, incluindo todas as propriedades de usuário que foram recuperadas, avaliadas ou gravadas como parte do evento hello.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Dicas para exibir hello provisionamento logs de auditoria

Para melhor legibilidade em Olá portal do Azure, selecione Olá **colunas** botão e escolha estas colunas:

* **Data** -mostra Olá data Olá evento ocorreu.
* **Destino (s)** -mostra Olá aplicativo nome e ID de usuário que são entidades de saudação do evento hello.
* **Atividade** -Olá tipo de atividade, conforme descrito anteriormente.
* **Status** : se o evento Olá foi bem-sucedida ou não.
* **Motivo do status** -um resumo do que aconteceu em Olá evento de provisionamento.


## <a name="troubleshooting"></a>Solucionar problemas

Olá, logs de auditoria e de relatório de resumo de provisionamento desempenha um papel fundamental ajudar administradores a solucionar vários problemas de provisionamento de conta de usuário.

Para obter orientação sobre como baseada em cenário tootroubleshoot automática provisionamento de usuário, consulte [problemas de configuração e provisionamento de aplicativo do usuário tooan](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
