---
title: aaaGet iniciado com a auditoria de banco de dados SQL do Azure | Microsoft Docs
description: "Introdução à auditoria do banco de dados SQL do Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>Introdução à auditoria do banco de dados SQL
Auditoria de banco de dados SQL Azure rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure. A auditoria também:

* Ajuda você a manter a conformidade regulatória, entender a atividade do banco de dados e obter informações sobre discrepâncias e anomalias que podem indicar preocupações para os negócios ou suspeitas de violações de segurança.

* Habilita e facilita a padrões de toocompliance aderência, embora ela não garante conformidade. Para obter mais informações sobre o Azure programas que conformidade com padrões de suporte, consulte Olá [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Visão geral da auditoria do banco de dados SQL do Azure
É possível usar a auditoria do banco de dados SQL para:


* **Retenha** uma trilha de auditoria dos eventos selecionados. Você pode definir categorias de banco de dados ações toobe auditado.
* **Relate** sobre a atividade do banco de dados. Você pode usar relatórios pré-configurados e um tooget painel iniciada rapidamente com a atividade e o relatório de eventos.
* **Analise** relatórios. Encontrar eventos suspeitos, atividades incomuns e tendências.

Você pode configurar a auditoria para diferentes tipos de categorias de evento, conforme explicado em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção.

Logs de auditoria são gravados tooAzure armazenamento de Blob em sua assinatura do Azure.


## <a id="subheading-8"></a>Definir a política de auditoria no nível do servidor versus no nível do banco de dados

Uma política de auditoria pode ser definida para um banco de dados específico ou como uma política padrão de servidor:

* Uma política de servidor se aplica a tooall existente e bancos de dados recém-criado no servidor de saudação.

* Se *auditoria de blob do servidor é habilitada*, ele *sempre aplica-se o banco de dados toohello* (ou seja, banco de dados hello será auditado), independentemente do banco de dados de saudação configurações de auditoria.

* Habilitar a auditoria no banco de dados do hello em adição tooenabling-lo no servidor de saudação do blob será *não* substituir ou alterar qualquer uma das configurações de saudação de auditoria de blob do servidor de saudação. Ambas as auditorias existirão lado a lado. Em outras palavras, o banco de dados de saudação será auditado duas vezes em paralelo (uma vez pela política do servidor de saudação e uma vez pela política de banco de dados de saudação).

   > [!NOTE]
   > Evite habilitar a auditoria de blobs de servidor e a auditoria de blobs do banco de dados juntas, a menos que:
    > * Você deseja toouse outro *conta de armazenamento* ou *período de retenção* para um banco de dados específico.
    > * Você deseja tooaudit tipos de evento ou categorias para um banco de dados que são diferentes dos tipos de eventos ou as categorias que estão sendo auditadas restante de saudação de bancos de dados Olá no servidor de saudação. Por exemplo, você pode ter inserções de tabela que precisa toobe auditada somente para um banco de dados específico.
   > 
   > Caso contrário, é recomendável que você habilite a auditoria de nível de servidor apenas blob e deixe Olá nível de banco de dados auditoria desabilitada para todos os bancos de dados.


## <a id="subheading-2"></a>Configurar a auditoria do banco de dados
Olá, seção a seguir descreve configuração Olá de auditoria usando Olá portal do Azure.

1. Vá toohello [portal do Azure](https://portal.azure.com).
2. Vá toohello **configurações** folha de saudação do banco de dados/SQL server SQL você deseja tooaudit. Em Olá **configurações** folha, selecione **detecção de auditoria e ameaças**.

    <a id="auditing-screenshot"></a> ![Painel de navegação][1]
3. Se você preferir tooset uma política de auditoria de servidor (que será aplicada tooall existente e bancos de dados recém-criado neste servidor), você pode selecionar Olá **exibir configurações de servidor** link na folha de auditoria de banco de dados de saudação. Você pode exibir ou modificar as configurações de auditoria de servidor de saudação.

    ![Painel de navegação][2]
4. Se você preferir tooenable blob auditoria no nível de banco de dados de saudação (em adição tooor em vez de auditoria de nível de servidor), para **auditoria**, selecione **ON**e para **auditoria tipo** , selecione **Blob**.

    Se o servidor blob auditoria estiver habilitada, a auditoria de banco de dados configurado de saudação existirá lado a lado com a auditoria de blob do servidor de saudação.  

    ![Painel de navegação][3]
5. Olá tooopen **armazenamento de Logs de auditoria** folha, selecione **detalhes de armazenamento**. Selecione a conta de armazenamento do Azure Olá onde os logs serão salvas e, em seguida, selecione o período de retenção hello, após o qual Olá logs antigos serão excluídos. Em seguida, clique em **OK**. 
   >[!TIP] 
   >Olá tooget máximo de modelos de relatórios auditoria hello, use Olá a mesma conta de armazenamento para todos os bancos de dados auditados. 

    <a id="storage-screenshot"></a> ![Painel de navegação][4]
6. Se você quiser toocustomize eventos de saudação auditado, você pode fazer isso por meio do PowerShell ou Olá API REST. Para obter mais detalhes, consulte Olá [automação (API REST/PowerShell)](#subheading-7) seção.
7. Depois de configurar as configurações de auditoria, você pode ativar o novo recurso de detecção de ameaças hello e configurar alertas de segurança de tooreceive de emails. Ao usar a detecção de ameaças, você recebe alertas proativos sobre atividades anômalas do banco de dados que podem indicar possíveis ameaças à segurança. Para obter mais detalhes, consulte [Introdução à detecção de ameaças](sql-database-threat-detection-get-started.md).
8. Clique em **Salvar**.





## <a id="subheading-3"></a>Analisar os logs e relatórios de auditoria
Logs de auditoria são agregados no hello escolhido durante a instalação de conta de armazenamento do Azure. Explore os logs de auditoria usando uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).

Os logs de auditoria de blob são salvos como uma coleção de arquivos de blob em um contêiner chamado **sqldbauditlogs**.

Para obter mais detalhes sobre a hierarquia de saudação da pasta de armazenamento de logs de auditoria de blob hello, convenções de nomenclatura de blob e formato de log, consulte Olá [Blob Audit Log formato referência (download do arquivo. docx)](https://go.microsoft.com/fwlink/?linkid=829599).

Há vários métodos que você pode usar o blob tooview logs de auditoria:

* Saudação de uso [portal do Azure](https://portal.azure.com).  Banco de dados relevante Olá aberto. AT Olá superior do banco de dados Olá **detecção de auditoria e ameaças** folha, clique em **exibir logs de auditoria**.

    ![Painel de navegação][7]

    Um **registros de auditoria** abre folha, do qual você será capaz de tooview Olá logs.

    - Você pode exibir datas específicas clicando **filtro** na parte superior de saudação do hello **registros de auditoria** folha.
    - Alterne entre os registros de auditoria que foram criados por uma auditoria da política de servidor ou da política de banco de dados.

       ![Painel de navegação][8]

* Use a função de sistema hello **sys. fn_get_audit_file** dados de log de auditoria (T-SQL) tooreturn Olá em formato tabular. Para obter mais informações sobre como usar essa função, consulte Olá [documentação de sys. fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Use a opção **Mesclar Arquivos de Auditoria** no SQL Server Management Studio (a partir do SSMS 17):  
    1. No menu do SSMS hello, selecione **arquivo** > **abrir** > **mesclar arquivos de auditoria**.

        ![Painel de navegação][9]
    2. Olá **adicionar arquivos de auditoria** caixa de diálogo é aberta. Selecione uma saudação **adicionar** opções se auditoria toomerge arquivos de um local de disco ou importá-los do armazenamento do Azure (será necessário tooprovide seus detalhes de armazenamento do Azure e a chave de conta).

    3. Depois de toomerge de todos os arquivos foram adicionados, clique em **Okey** toocomplete operação de mesclagem de saudação.

    4. arquivo mesclado Olá abre no SSMS, onde você pode exibir e analisá-lo, bem como a exportação-tooan XEL ou CSV arquivo ou tooa tabela.

* Saudação de uso [sincronizar aplicativo](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que você criou. Ele é executado no Azure e utiliza a análise de Log do Operations Management Suite (OMS) pública APIs toopush SQL logs de auditoria ao OMS. aplicativo de sincronização Hello envia logs de auditoria do SQL em análise de logs do OMS para consumo por meio do painel de análise de logs do OMS hello. 

* Use o Power BI. Você pode exibir e analisar dados do log de auditoria no Power BI. Saiba mais sobre o [Power BI e acesse um modelo para download](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Baixar arquivos de log do seu contêiner de blob de armazenamento do Azure por meio do portal hello, ou usando uma ferramenta como [Azure Storage Explorer](http://storageexplorer.com/).
    * Depois de baixar um arquivo de log localmente, você pode clicar duas vezes tooopen do arquivo hello, exibir e analisar logs Olá no SSMS.
    * Baixe também vários arquivos simultaneamente por meio do Gerenciador de Armazenamento do Azure. Clique em uma subpasta específica (por exemplo, uma subpasta que inclui todos os arquivos de log para uma data específica) e selecione **Salvar como** toosave em uma pasta local.

* Métodos adicionais:
   * Depois de baixar vários arquivos (ou em uma subpasta que inclui arquivos de log para um dia inteiro, conforme descrito no item anterior Olá nesta lista), você pode mesclá-los localmente conforme descrito nas instruções de arquivos de auditoria de mesclagem do SSMS Olá descritas anteriormente.

   * Exiba os logs de auditoria de blob de forma programática:

     * Saudação de uso [leitor de eventos estendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteca C#.
     * [Consulte Arquivos de Eventos Estendidos usando o PowerShell](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/).




## <a id="subheading-5"></a>Práticas de produção
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Auditoria de bancos de dados replicados geograficamente</a>
Quando você usa os bancos de dados replicada geograficamente, é possível tooset a auditoria no banco de dados primário Olá, banco de dados secundário hello ou ambos, dependendo do tipo de auditoria de saudação.

Siga estas instruções (Lembre-se de que a auditoria de blob pode ser ativada ou desativada somente de banco de dados primário Olá configurações de auditoria):

* **Banco de dados primário**. Ativar a auditoria de blob, no servidor de saudação ou Olá próprio banco de dados, conforme descrito em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção.
* **Banco de dados secundário**. Ativar a auditoria de blob no banco de dados primário hello, conforme descrito em Olá [configurar a auditoria para seu banco de dados](#subheading-2) seção. 
   * Auditoria de blob deve ser habilitada nos Olá *banco de dados primário em si*, não o servidor de saudação.
   * Depois que a auditoria de blob estiver habilitada no banco de dados primário hello, ele também será habilitado no banco de dados secundário hello.

     >[!IMPORTANT]
     >Por padrão, as configurações de armazenamento Olá para o banco de dados secundário Olá será idêntico toothose do banco de dados primário Olá, fazendo com que o tráfego entre regional. Você pode evitar isso, permitindo a auditoria de blob no servidor secundário hello e configurar o armazenamento local nas configurações de armazenamento do servidor secundário Olá. Isso substituirá o local de armazenamento de saudação para o banco de dados secundário hello e resultam em cada banco de dados salvando seu armazenamento de toolocal de logs de auditoria.  
<br>

### <a id="subheading-6">Regeneração de chave de armazenamento</a>
Em produção, você está provavelmente toorefresh o armazenamento de chaves periodicamente. Ao atualizar as chaves, é necessário a diretiva de auditoria tooresave hello. processo de saudação é o seguinte:

1. Olá abrir **armazenamento detalhes** folha. Em Olá **chave de acesso de armazenamento** selecione **secundário**e clique em **Okey**. Em seguida, clique em **salvar** na parte superior de saudação do hello folha de configuração de auditoria.

    ![Painel de navegação][5]
2. Vá toohello folha de configuração de armazenamento e regenerar a chave de acesso primária hello.

    ![Painel de navegação][6]
3. Voltar toohello folha de configuração de auditoria, alternar a chave de acesso de armazenamento de saudação do tooprimary secundário e, em seguida, clique em **Okey**. Em seguida, clique em **salvar** na parte superior de saudação do hello folha de configuração de auditoria.
4. Volte toohello folha de configuração de armazenamento e chave de acesso secundária Olá regenerar (em preparação para o ciclo de atualização da chave Olá próximo).

## <a id="subheading-7"></a>Automação (PowerShell/API REST)
Você também pode configurar a auditoria no banco de dados do SQL Azure usando Olá ferramentas de automação a seguir:

* **Cmdlets do PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   Para obter um exemplo de script, confira [Configurar a auditoria e a detecção de ameaças usando o PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **API REST – Auditoria de blob**:

   * [Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Criar ou atualizar a política de auditoria de blob do banco de dados)
   * [Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Criar ou atualizar uma política de auditoria de blob de servidor)
   * [Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obter a política de auditoria de blob do banco de dados)
   * [Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obter a política de auditoria de blob do servidor)
   * [Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obter o resultado da operação de auditoria do blob do servidor)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
