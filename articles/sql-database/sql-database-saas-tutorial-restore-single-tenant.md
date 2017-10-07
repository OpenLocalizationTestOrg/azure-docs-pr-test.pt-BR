---
title: "aaaRestore um banco de dados do SQL Azure em um aplicativo multilocatário | Microsoft Docs"
description: "Saiba como toorestore um único locatários SQL banco de dados após a exclusão acidental de dados"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Restaurar um banco de dados SQL de locatários de Wingtip SaaS

aplicativo de SaaS Wingtip Olá é criado usando um modelo de banco de dados por locatário, onde cada locatário tem seu próprio banco de dados. Um dos benefícios de saudação desse modelo é que ele é fácil toorestore dados de um único locatário em isolamento sem afetar outros locatários.

Neste tutorial, você aprenderá dois padrões de recuperação de dados:

> [!div class="checklist"]

> * Restaurar um banco de dados em um banco de dados paralelo (lado a lado)
> * Restaurar um banco de dados no local


|||
|:--|:--|
| **Restaurar locatário tooa anterior ponto no tempo, em um banco de dados paralelo** | Esse padrão pode ser usado por locatário Olá para revisão, auditoria, conformidade, o banco de dados original etc. Olá permaneça online e inalterados. |
| **Restaurar locatário no local** | Esse padrão é geralmente usado toorecover um ponto anterior do locatário tooa no tempo, depois que um locatário exclui acidentalmente os dados. banco de dados original Olá é colocado offline e substituído pelo banco de dados restaurado hello. |
|||

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Padrão de restauração Introdução toohello SaaS locatário

Por locatário Olá restaurar padrão, há dois padrões de simples para restaurar dados de um locatário individual. Como os bancos de dados de locatário são isolados uns dos outros, restaurar um locatário não afeta os dados de outro locatário.

No padrão da primeira hello, os dados são restaurados em um novo banco de dados. locatário Olá recebe banco de dados do access toothis juntamente com os dados de produção. Esse padrão permite que um locatário dados do administrador tooreview Olá restaurado e usá-lo tooselectively substituir valores de dados atual. É o toohello SaaS aplicativo designer toodetermine como sofisticado hello opções devem ser a recuperação de dados. Simplesmente tooreview capaz de dados em estado de saudação que se encontrava em um determinado ponto no tempo pode ser tudo o que é necessário em alguns cenários. Se o banco de dados de saudação usa [replicação geográfica](sql-database-geo-replication-overview.md), é recomendável copiar dados necessários de saudação da cópia Olá restaurado no banco de dados original hello. Se você substituir o banco de dados original Olá com banco de dados de saudação restaurado, você precisa tooreconfigure e ressincronizar a replicação geográfica.

No padrão de segundo hello, que assume locatário Olá sofreu uma perda ou corrupção de dados, banco de dados de produção de hello locatário é restaurado tooa o ponto anterior no tempo. Olá restauração no local padrão, locatário Olá é colocado offline por um curto período enquanto o banco de dados de saudação é restaurado e colocado online novamente. Olá banco de dados original é excluído, mas ainda podem ser restaurado se você precisar tooan back toogo anterior mesmo ponto no tempo. Uma variação desse padrão foi possível renomear o banco de dados de saudação em vez de excluí-lo, embora o banco de dados renomeando Olá oferece vantagens adicionais em termos de segurança de dados.

## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Simular um locatário excluindo acidentalmente os dados

toodemonstrate esses cenários de recuperação, é preciso muito*acidentalmente* excluir alguns dados em um dos bancos de dados de locatário hello. Enquanto você pode excluir qualquer registro, Olá próxima etapa configura Olá demonstração toonot é bloqueada por violações de integridade referencial! Ele também adiciona alguns dados de tíquete de compra você pode usar mais tarde no hello *tutoriais de análise de SaaS Wingtip*.

Executar script do gerador de tíquete hello e criar dados adicionais. Gerador de tíquete Olá intencionalmente não comprar ingressos para cada evento última locatários.

1. Abrir... \\Módulos de aprendizado\\utilitários\\*demonstração TicketGenerator.ps1* em Olá *PowerShell ISE*
1. Pressione **F5** toorun Olá script e gerar clientes e dados de vendas de tíquete.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Abra os eventos da atuais de Olá Olá eventos aplicativo tooreview

1. Olá abrir *Hub de eventos* (http://events.wtp.&lt; usuário&gt;. trafficmanager.net) e clique em **Contoso conjunto Hall**:

   ![hub de eventos](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Role a lista de saudação de eventos e tome nota do último evento de saudação na lista de saudação:

   ![último evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Executar Olá demonstração cenário tooaccidentally Olá último evento delete

1. Abrir... \\Módulos de aprendizado\\continuidade dos negócios e recuperação de desastres\\RestoreTenant\\*demonstração RestoreTenant.ps1* em Olá *PowerShell ISE*, e o conjunto Olá seguinte valor:
   * **$DemoScenario** = **1**, defina muito**1** -excluir eventos sem vendas de tíquete.
1. Pressione **F5** toorun Olá script e excluir o último evento de saudação. Você verá uma confirmação mensagem semelhante toohello a seguir:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. Olá Contoso eventos página é aberta. Role para baixo e verifique se o evento Olá será excluído. Se o evento Olá ainda está em lista Olá, clique em atualizar e verificar será excluída.

   ![último evento](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Restaurar um banco de dados de locatário em paralelo com o banco de dados de produção de hello

Este exercício restaura o ponto de tooa Olá Contoso conjunto Hall banco de dados no tempo antes do evento Olá foi excluído. Após a exclusão evento Olá nas etapas anteriores hello, você deseja toorecover e ver dados Olá excluído. Você não precisa toorestore seu banco de dados de produção com registro Olá excluído, mas você precisa toorecover Olá antigo banco de dados tooaccess Olá dados antigos por outros motivos comerciais.

 Olá *restauração TenantInParallel.ps1* script cria um locatário paralelo banco de dados e uma catálogo paralela entrada ambos os denominado *ContosoConcertHall\_antigo*. Esse padrão de restauração é mais adequado para a recuperação de uma perda de dados pequena ou para cenários de recuperação de conformidade e auditoria. Também é Olá abordagem recomendada quando você estiver usando [georeplicação](sql-database-geo-replication-overview.md).

1. Olá completa [simular um usuário excluir acidentalmente dados](#simulate-a-tenant-accidentally-deleting-data) seção.
1. Abrir... \\Módulos de aprendizado\\continuidade dos negócios e recuperação de desastres\\RestoreTenant\\_demonstração RestoreTenant.ps1_ em Olá *PowerShell ISE*.
1. Definir **$DemoScenario** = **2**, defina esta opção muito**2** muito*restauração locatário em paralelo*.
1. Pressione **F5** toorun script de saudação.

script Hello restaura Olá locatário database (banco de dados tooa paralela) tooa ponto no tempo antes da exclusão de eventos de saudação na seção anterior hello. Ele cria um segundo banco de dados, remove os metadados de catálogo existentes que existe neste banco de dados e adiciona o catálogo de toohello do banco de dados de saudação em Olá *ContosoConcertHall\_antigo* entrada.

script de demonstração de Olá abre a página de eventos de saudação em seu navegador. Observação de URL Olá: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` que isso está mostrando os dados do banco de dados restaurado de saudação onde *old* é adicionado toohello nome.

Rolagem Olá eventos listados no hello navegador tooconfirm Olá eventos excluídos na seção anterior Olá foi restaurado.

Observe expondo locatário Olá restaurado como um locatário adicional, com permissões de toobrowse seu próprio aplicativo eventos, é improvável que toobe como você deve fornecer que um locatário acessar toorestored dados, mas serve tooeasily ilustra padrão de restauração hello.

Na realidade, você provavelmente manteria esse banco de dados restaurado somente por um período definido. Você pode excluir a entrada de locatário de saudação restaurada depois que você terminou por chamada hello *remover RestoredTenant.ps1* script.

1. Definir **$DemoScenario** muito**4** tooselect Olá *remover restaurado locatário* cenário.
1. **Execute** **usando** **F5**
1. Olá *ContosoConcertHall\_antigo* entrada agora é excluída do catálogo de saudação. Vá em frente e feche a página de eventos de saudação para este locatário em seu navegador.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Restaurar um locatário em vigor, substituindo o banco de dados do locatário existente Olá

Este exercício restaura um ponto de tooa Olá Contoso conjunto Hall locatário tempo antes do evento Olá foi excluído. Olá *TenantInPlace restauração* restaura o script hello locatário banco de dados tooa novo banco de dados atual apontando ponto anterior tooa no tempo e exclusões Olá banco de dados original. Esse padrão de restauração é mais adequado para a recuperação de corrupção de dados grave pois pode haver perda de dados significativos Olá locatário teria tooaccommodate.

1. Abra o arquivo **Demo-RestoreTenant.ps1** no ISE do PowerShell
1. Definir **$DemoScenario** muito**5** tooselect Olá *locatário no cenário de local de restauração*.
1. Execute usando **F5**.

script Hello restaura o ponto de tooa de banco de dados de locatário Olá cinco minutos antes de saudação evento foi excluído. Ele faz isso primeiro colocar Olá Contoso conjunto Hall locatário off-line para que não há nenhuma outra atualiza toohello dados. Em seguida, um banco de dados paralelo é criado pela restauração do ponto de restauração hello e nomeado com um carimbo de hora nome de banco de dados de saudação tooensure não está em conflito com o nome de banco de dados de locatário existente do hello. Em seguida, banco de dados de locatário antiga Olá é excluído e Olá banco de dados restaurado é o nome do banco de dados original renomeado toohello. Por fim, Contoso conjunto Hall é colocado online tooallow Olá aplicativo toohello restaurado banco de dados.

Você restaurou com êxito Olá banco de dados tooa ponto no tempo antes do evento Olá foi excluído. Olá abre da página de eventos, portanto confirme último evento de saudação foi restaurado.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]

> * Restaurar um banco de dados em um banco de dados paralelo (lado a lado)
> * Restaurar um banco de dados no local

[Gerenciar o esquema de banco de dados do locatário](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais que se baseiam na Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Visão geral da continuidade dos negócios com o Banco de Dados SQL do Azure](sql-database-business-continuity.md)
* [Saiba mais sobre o Banco de Dados SQL](sql-database-automated-backups.md)
