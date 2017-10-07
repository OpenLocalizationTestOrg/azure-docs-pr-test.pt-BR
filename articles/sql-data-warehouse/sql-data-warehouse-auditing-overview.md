---
title: aaaAuditing no Azure SQL Data Warehouse | Microsoft Docs
description: "Introdução à auditoria no SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Auditoria no Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Auditoria](sql-data-warehouse-auditing-overview.md)
> * [Detecção de ameaças](sql-data-warehouse-security-threat-detection.md)
> 
> 

Auditoria do SQL Data Warehouse permite toorecord eventos no log de auditoria de banco de dados tooan em sua conta de armazenamento do Azure. A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança. A auditoria do SQL Data Warehouse também se integra ao Microsoft Power BI para relatórios e análises de buscas detalhadas.

Ferramentas de auditoria habilitar e facilitar os padrões toocompliance aderência mas não garantem a conformidade. Para obter mais informações sobre o Azure programas que conformidade com padrões de suporte, consulte Olá <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.

* [Fundamentos da Auditoria do Banco de Dados]
* [Configurar a auditoria do banco de dados]
* [Analisar os logs e relatórios de auditoria]

## <a id="subheading-1"></a>Fundamentos da Auditoria do Banco de Dados do SQL Data Warehouse do Azure
A auditoria do banco de dados do SQL Data Warehouse permite que você:

* **Retenha** uma trilha de auditoria dos eventos selecionados. Você pode definir categorias de banco de dados ações toobe auditado.
* **Relate** sobre a atividade do banco de dados. Você pode usar relatórios pré-configurados e um tooget painel iniciada rapidamente com a atividade e o relatório de eventos.
* **Analise** relatórios. Encontrar eventos suspeitos, atividades incomuns e tendências.

Você pode configurar a auditoria de saudação categorias de evento a seguir:

**SQL simples** e **SQL parametrizadas** para qual Olá logs de auditoria coletados são classificados como  

* **Toodata de acesso**
* **Alterações de esquema (DDL)**
* **Alterações de dados (DML)**
* **Contas, funções e permissões (DCL)**
* **Procedimento armazenado**, **Logon** e **Gerenciamento de transações**.

Para cada categoria de evento, as operações de auditoria de **sucesso** e **falha** são configuradas separadamente.

Para obter mais informações sobre atividades hello e eventos de auditoria, consulte Olá <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referência de formato de Log de auditoria (download do arquivo doc)</a>.

Logs de auditoria são armazenados na sua conta de armazenamento do Azure. Você pode definir um período de retenção para logs de auditoria.

Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão do servidor. Uma política de auditoria de servidor padrão se aplica a bancos de dados tooall em um servidor, que não têm uma substituição de banco de dados auditoria política específica definida.

Antes de configurar a auditoria, verifique se você está usando um ["Cliente de nível inferior"](sql-data-warehouse-auditing-downlevel-clients.md).

## <a id="subheading-2"></a>Configurar a auditoria do banco de dados
1. Iniciar Olá <a href="https://portal.azure.com" target="_blank">portal do Azure</a>.
2. Vá toohello **configurações** folha de saudação SQL Data Warehouse, você deseja tooaudit. Em Olá **configurações** folha, selecione **detecção de auditoria e ameaças**.
   
    ![][1]
3. Em seguida, habilitar a auditoria clicando Olá **ON** botão.
   
    ![][3]
4. No hello folha de configuração de auditoria, selecione **detalhes armazenamento** tooopen folha de armazenamento de Logs de auditoria de saudação. Selecione Olá conta de armazenamento do Azure onde os logs serão salvas e hello período de retenção. 
>[!TIP]
>Olá Use pré-configurado de mesma conta de armazenamento para todos os Olá de tooget auditados bancos de dados máximo Olá relatórios de modelos.
   
    ![][4]
5. Clique em Olá **Okey** configuração detalhes de armazenamento de saudação do botão toosave.
6. Em **registro em log pelo evento**, clique em **êxito** e **falha** toolog todos os eventos, ou escolha categorias de evento individuais.
7. Se você estiver configurando a auditoria para um banco de dados, talvez seja necessário cadeia de caracteres de conexão Olá de tooalter de sua tooensure cliente dados de auditoria é capturado corretamente. Verificar Olá [modificar o FQDN do servidor na cadeia de caracteres de conexão Olá](sql-data-warehouse-auditing-downlevel-clients.md) tópico para conexões de cliente de nível inferior.
8. Clique em **OK**.

## <a id="subheading-3"></a>Analisar os logs e relatórios de auditoria
Logs de auditoria são agregados em uma coleção de tabelas de armazenamento com uma **SQLDBAuditLogs** prefixo no hello escolhido durante a instalação de conta de armazenamento do Azure. Você pode ver os arquivos de log usando uma ferramenta como o <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Gerenciador de Armazenamento do Azure</a>.

Um modelo de relatório do painel pré-configurado está disponível como um <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">planilha do Excel para download</a> toohelp você analisar rapidamente os dados de log. modelo de saudação toouse em seus logs de auditoria, você precisa Excel 2013 ou posterior e o Power Query, que você pode baixar <a href="http://www.microsoft.com/download/details.aspx?id=39379">aqui</a>.

Olá possui dados de exemplo fictício nele, e você pode configurar tooimport Power Query seu log de auditoria diretamente de sua conta de armazenamento do Azure.

## <a id="subheading-4"></a>Regeneração de chave de armazenamento
Em produção, você está provavelmente toorefresh o armazenamento de chaves periodicamente. Ao atualizar as chaves, é necessário toosave política de saudação. processo de saudação é o seguinte:

1. No hello auditoria folha de configuração (instalação Olá auditoria seção descrita acima), alterne Olá **chave de acesso de armazenamento** de *primário* muito*secundário* e  **Salvar**.

   ![][4]
2. Folha de configuração de armazenamento vá toohello e **regenerar** Olá *chave de acesso primário*.
3. Voltar toohello auditoria folha de configuração de comutador hello **chave de acesso de armazenamento** de *secundário* muito*primário* e pressione **salvar**.
4. Voltar toohello armazenamento da interface do usuário e **regenerar** Olá *chave de acesso secundária* (como preparação para Olá chaves próximas ciclo de atualização.

## <a id="subheading-5"></a>Automação (PowerShell/API REST)
Você também pode configurar a auditoria no Azure SQL Data Warehouse usando Olá ferramentas de automação a seguir:

* **Cmdlets do PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Fundamentos da Auditoria do Banco de Dados]: #subheading-1
[Configurar a auditoria do banco de dados]: #subheading-2
[Analisar os logs e relatórios de auditoria]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy