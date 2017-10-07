---
title: "pesquisas de log aaaComputer grupos na análise de Log | Microsoft Docs"
description: "Grupos de computadores na análise de Log permitem que você tooscope log pesquisas tooa determinado conjunto de computadores.  Este artigo descreve métodos diferentes hello, você pode usar grupos de computadores toocreate e como toouse-los em um log de pesquisa."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Grupos de computadores em pesquisas de log do Log Analytics

>[!NOTE]
> Este artigo descreve o uso de saudação de grupos de computadores usando linguagem de consulta de Log Anayltics atual hello.    Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de nova análise de Log](log-analytics-log-search-upgrade.md), em seguida, grupos de computadores funcionam de forma diferente.  Anotações são fornecidas neste artigo com sintaxe diferente da saudação e comportamento Olá nova linguagem de consulta.  


Grupos de computadores na análise de Log permitem tooscope [pesquisas de log](log-analytics-log-searches.md) tooa determinado conjunto de computadores.  Cada grupo é preenchido com computadores usando uma consulta que você define ou importando grupos de fontes diferentes.  Quando hello está incluído em uma pesquisa de log, resultados Olá são limitados toorecords que correspondem a computadores de saudação do grupo de saudação.

## <a name="creating-a-computer-group"></a>Criando um grupo de computadores
Você pode criar um grupo de computadores na análise de Log usando qualquer um dos métodos de saudação em Olá a tabela a seguir.  Detalhes sobre cada método são fornecidos nas seções de saudação abaixo. 

| Método | Descrição |
|:--- |:--- |
| Pesquisa de log |Criar uma pesquisa de log que retorna uma lista de computadores e salvar os resultados de saudação como um grupo de computadores. |
| API da Pesquisa de Log |Use Olá API de pesquisa de Log tooprogrammatically criar um grupo de computadores com base nos resultados de saudação de uma pesquisa de log. |
| Active Directory |Verificar automaticamente a associação de grupo de saudação de todos os computadores agente que são membros de um domínio do Active Directory e criar um grupo em análise de Log para cada grupo de segurança. |
| WSUS |Verifique servidores ou clientes de WSUS para direcionar grupos e criar um grupo no Log Analytics para cada um. |

### <a name="log-search"></a>Pesquisa de log
Grupos de computadores criados a partir de uma pesquisa de Log contêm todos os computadores hello retornadas por uma consulta de pesquisa que você definir.  Essa consulta é executada sempre que o grupo de computadores Olá é usado para que as alterações desde que foi criado o grupo de saudação seja refletido.

Use Olá seguindo o procedimento toocreate um grupo de computadores de uma pesquisa de log.

1. [Crie uma pesquisa de log](log-analytics-log-searches.md) que retorna uma lista de computadores.  Olá pesquisa deve retornar um conjunto distinto de computadores usando algo como **computador distinto** ou **contagem pelo computador de medida** na consulta de saudação.  
2. Clique em Olá **salvar** botão na parte superior de saudação da tela hello.
3. Selecione **Sim** muito**salvar essa consulta como um grupo de computadores**.
4. Digite um **nome** e um **categoria** para grupo de saudação.  Se uma pesquisa com hello mesmo nome e categoria já existir, será solicitada toooverwrite-lo.  Você pode ter várias pesquisas com o mesmo nome em categorias diferentes de saudação. 

A seguir, temos pesquisas de exemplo que você pode salvar como um grupo de computadores.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md) hello, as seguintes alterações serão feitas toohello procedimento toocreate um novo grupo de computadores.
>  
> - Olá toocreate de consulta deve incluir um grupo de computadores `distinct Computer`.  A seguir está um exemplo de uma consulta de toocreate um grupo de computadores.<br>`Heartbeat | where Computer contains "srv" `
> - Quando você cria um novo grupo de computadores, você deve especificar um alias no nome de toohello de adição.  Use o alias de saudação ao usar o grupo de computadores de saudação em uma consulta conforme descrito abaixo.  

### <a name="log-search-api"></a>API da Pesquisa de Log
Grupos de computadores criados com hello API de pesquisa de Log são Olá mesmo como pesquisas criadas com uma pesquisa de Log.

Para obter detalhes sobre como criar um grupo de computadores usando a API de pesquisa de Log de saudação consulte [API REST de pesquisa de grupos de computadores no log de análise de Log](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Ao configurar associações de grupo do Active Directory de tooimport de análise de Log, ele analisa a associação de grupo de saudação de todos os computadores com o agente do OMS Olá ingressado no domínio.  Um grupo de computadores é criado na análise de Log para cada grupo de segurança no Active Directory, e cada computador é adicionado a grupos de computadores toohello correspondentes forem membros de grupos de segurança de toohello.  Essa associação é atualizada continuamente a cada 4 horas.  

Configurar grupos de segurança de Active Directory de tooimport de análise de Log da saudação **grupos de computadores** menu na análise de Log **configurações**.  Selecione **Automação** e **Importe as associações de grupo do Active Directory dos computadores**.  Não é necessária nenhuma configuração.

![Grupos de computadores do Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Quando grupos importados, hello menu listas Olá número de computadores com associação de grupo detectados e Olá número de grupos importados.  Você pode clicar em qualquer um dos Olá de tooreturn links **ComputerGroup** registros com essas informações.

### <a name="windows-server-update-service"></a>Serviços de Atualização do Windows Server
Quando você configurar as associações de grupo tooimport de análise de Log do WSUS, ele analisa Olá direcionando membros do grupo de todos os computadores com o agente do OMS Olá.  Se você estiver usando o cliente direcionamento, qualquer computador que está conectado tooOMS e faz parte de qualquer WSUS direcionamento grupos de sua associação de grupo importou tooLog análise. Se você estiver usando o servidor direcionamento, Olá agente do OMS deve ser instalado em Olá WSUS servidor Olá toobe de informações de associação de grupo importado tooOMS.  Essa associação é atualizada continuamente a cada 4 horas. 

Configurar grupos de segurança de Active Directory de tooimport de análise de Log da saudação **grupos de computadores** menu na análise de Log **configurações**.  Selecione **Active Directory** e **Importe as associações de grupo do Active Directory dos computadores**.  Não é necessária nenhuma configuração.

![Grupos de computadores do Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Quando grupos importados, hello menu listas Olá número de computadores com associação de grupo detectados e Olá número de grupos importados.  Você pode clicar em qualquer um dos Olá de tooreturn links **ComputerGroup** registros com essas informações.

## <a name="managing-computer-groups"></a>Gerenciando grupos de computadores
Você pode exibir grupos de computadores que foram criados a partir de uma pesquisa de log ou Olá API de pesquisa de Log de saudação **grupos de computadores** menu na análise de Log **configurações**.  Clique em Olá **x** em Olá **remover** grupo de computadores coluna toodelete hello.  Clique em Olá **exibir membros** ícone de pesquisa de log de um grupo toorun Olá grupo que retorna a seus membros. 

![Grupos de computadores salvados](media/log-analytics-computer-groups/configure-saved.png)

Olá toomodify grupo, crie um novo grupo com hello mesmo **categoria** e **nome** grupo original do toooverwrite hello.

## <a name="using-a-computer-group-in-a-log-search"></a>Usando um grupo de computadores em uma pesquisa de log
Usar o hello grupo de computadores sintaxe toorefer tooa em uma pesquisa de log a seguir.  Olá especificando **categoria** é opcional e somente necessário se você tiver grupos de computadores com o mesmo nome em categorias diferentes de saudação. 

    $ComputerGroups[Category: Name]

Quando uma pesquisa é executada, membros de saudação de quaisquer grupos de computadores incluídos na pesquisa de saudação são resolvidos primeiro.  Se o grupo de saudação baseia-se em uma pesquisa de log, que a pesquisa é executada tooreturn membros de saudação do grupo de saudação antes de executar a pesquisa de log de nível superior de saudação.

Grupos de computadores são usados normalmente com hello **IN** cláusula na pesquisa de log hello como Olá exemplo a seguir:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de nova análise de Log](log-analytics-log-search-upgrade.md), em seguida, usar um grupo de computadores em uma consulta tratando seu alias como uma função como Olá exemplo a seguir:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Registros de grupo de computadores
Um registro é criado no repositório do OMS Olá para cada associação de grupo do computador criado a partir do Active Directory ou do WSUS.  Esses registros têm um tipo de **ComputerGroup** e têm propriedades de saudação em Olá a tabela a seguir.  Registros não são criados para grupos de computadores com base em pesquisas de log.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Computador |Nome do computador do membro hello. |
| Agrupar |Nome do grupo de saudação. |
| GroupFullName |Grupo de toohello de caminho completo incluindo fonte hello e o nome da fonte. |
| GroupSource |Fonte da qual o grupo foi coletado. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nome da fonte Olá Olá grupo de foram coletado do.  Para o Active Directory, esse é o nome de domínio de saudação. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes SCOM.  Para outros agentes, ele é AOI-\<ID do espaço de trabalho\> |
| TimeGenerated |Grupo de computadores de data e hora Olá foi criado ou atualizado. |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.  

