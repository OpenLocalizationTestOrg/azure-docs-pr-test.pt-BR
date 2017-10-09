---
title: "aaaManaging dados de automação do Azure | Microsoft Docs"
description: "Este artigo contém vários tópicos sobre o gerenciamento de um ambiente da Automação do Azure.  Atualmente, inclui a Retenção de dados e o backup da Recuperação de desastres na Automação do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Gerenciando dados da Automação do Azure
Este artigo contém vários tópicos sobre o gerenciamento de um ambiente da Automação do Azure.

## <a name="data-retention"></a>Retenção de dados
Quando você exclui um recurso na Automação do Azure, ele é retido por 90 dias para fins de auditoria antes de ser removido permanentemente.  Você não pode ver ou usar o recurso de saudação durante esse tempo.  Essa política também se aplica a tooresources que pertencem a conta de automação de tooan é excluída.

A Automação do Azure exclui de forma automática e remove de forma permanente os trabalhos com mais de 90 dias.

Olá, a tabela a seguir resume a política de retenção de saudação para recursos diferentes.

| Dados | Política |
|:--- |:--- |
| Contas |Removido de forma permanente 90 dias depois Olá conta é excluída por um usuário. |
| Ativos |Removido de forma permanente 90 dias após Olá ativo é excluído por um usuário ou 90 dias após Olá conta que contém o ativo de saudação é excluída por um usuário. |
| Módulos |Removido de forma permanente 90 dias após o módulo de saudação é excluído por um usuário ou 90 dias após Olá conta que contém o módulo de saudação é excluída por um usuário. |
| Runbooks |Removido de forma permanente 90 dias após Olá recurso for excluído por um usuário ou 90 dias após Olá conta que contém o recurso de saudação é excluída por um usuário. |
| Trabalhos |Excluído e removidos permanentemente 90 dias após a última modificação. Isso pode ocorrer após Olá trabalho for concluído, é interrompido ou está suspenso. |
| Arquivos de configurações/MOF de nó |A configuração de nó antigo é removida permanentemente 90 dias depois que uma nova configuração de nó é gerada. |
| Nós DSC |Removido de forma permanente 90 dias após o nó hello está registrado da conta de automação usando o portal do Azure ou Olá [AzureRMAutomationDscNode Unregister](https://msdn.microsoft.com/library/mt603500.aspx) cmdlet do Windows PowerShell. Nós são também permanentemente excluídos 90 dias após a conta de saudação que contém o nó de saudação é excluído por um usuário. |
| Relatórios de Nó |Removido de forma permanente 90 dias depois que um novo relatório é gerado para esse nó |

política de retenção Olá aplica tooall usuários e atualmente não pode ser personalizada.

No entanto, se você precisar tooretain dados para um período de tempo maior, você pode encaminhar tooLog de logs de trabalho de runbook análise.  Para obter mais informações, consulte [encaminhar tooOMS de dados de trabalho de automação do Azure Log Analytics](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Fazendo backup da Automação do Azure
Quando você exclui uma conta de automação no Microsoft Azure, todos os objetos na conta de saudação são excluídos incluindo runbooks, módulos, configurações, as configurações, trabalhos e ativos. objetos de saudação não podem ser recuperados depois Olá conta é excluída.  Você pode usar o hello conteúdo de saudação toobackup informações de sua conta de automação a seguir antes de excluí-lo. 

### <a name="runbooks"></a>Runbooks
Você pode exportar os arquivos de tooscript runbooks usando Olá Portal de gerenciamento ou hello [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) cmdlet do Windows PowerShell.  Esses arquivos de script podem ser importados para outra conta de automação, conforme discutido em [Criando ou importando um runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Módulos de integração
Você não pode exportar módulos de integração da Automação do Azure.  Você deve garantir que estejam disponíveis fora da conta de automação de saudação.

### <a name="assets"></a>Ativos
Não é possível exportar [ativos](https://msdn.microsoft.com/library/dn939988.aspx) da Automação do Azure.  Usando Olá Portal de gerenciamento, você deve anotar os detalhes de saudação de variáveis, credenciais, certificados, conexões e agendas.  Você deve criar manualmente qualquer ativo que seja usado por runbooks importados para outra automação.

Você pode usar [cmdlets do Azure](https://msdn.microsoft.com/library/dn690262.aspx) detalhes tooretrieve do ativos não criptografados e salvá-los para um futuro referência ou criar ativos equivalentes em outra conta de automação.

Não é possível recuperar o valor de saudação para variáveis criptografadas ou campo de senha de saudação de credenciais usando os cmdlets.  Se você não souber esses valores, você pode recuperá-los de um runbook usando Olá [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) e [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) atividades.

Você não pode exportar certificados da Automação do Azure.  Você deve garantir que todos os certificados estejam disponíveis fora do Azure.

### <a name="dsc-configurations"></a>Configurações DSC
Você pode exportar configurações tooscript arquivos usando Olá Portal de gerenciamento ou hello [AzureRmAutomationDscConfiguration de exportação](https://msdn.microsoft.com/library/mt603485.aspx) cmdlet do Windows PowerShell. Essas configurações podem ser importadas e usadas em outra conta de automação.

## <a name="geo-replication-in-azure-automation"></a>Replicação geográfica na Automação do Azure
Replicação geográfica, padrão em contas de automação do Azure, o backup conta dados tooa diferentes região geográfica para redundância. Você pode escolher uma região primária ao configurar sua conta e, em seguida, uma região secundária é atribuída tooit automaticamente. os dados secundários de Hello, copiados da região primária do hello, são atualizados continuamente em caso de perda de dados.  

Olá, a tabela a seguir mostra os emparelhamentos de região primária e secundária disponível de saudação.

| Primário | Secundário |
| --- | --- |
| Centro-Sul dos Estados Unidos |Centro-Norte dos EUA |
| Leste dos EUA 2 |Centro dos EUA |
| Europa Ocidental |Norte da Europa |
| Sudeste da Ásia |Ásia Oriental |
| Leste do Japão |Oeste do Japão |

Olá improvável que uma região primária de dados é perdidos, Microsoft tenta toorecovê-lo. Dados primários Olá não puderem ser recuperados, em seguida, failover geográfico é executado e hello clientes afetados serão notificados sobre isso através de sua assinatura.

