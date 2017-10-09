---
title: "solução de aaaOffice 365 no OMS Operations Management Suite () | Microsoft Docs"
description: "Este artigo fornece detalhes sobre a configuração e o uso da solução Olá Office 365 no OMS.  Ele inclui uma descrição detalhada dos registros de saudação Office 365 criados na análise de Log."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>A solução do Office 365 no OMS (Operations Management Suite)

![Logotipo do Office 365](media/oms-solution-office-365/icon.png)

Olá solução do Office 365 para o Operations Management Suite (OMS) permite que você toomonitor seu ambiente do Office 365 em análise de Log.  

- Monitorar atividades do usuário em seus padrões de uso de tooanalyze de contas do Office 365, bem como identificar tendências de comportamentos. Por exemplo, você pode extrair os cenários de uso específicos, como arquivos que são compartilhados fora da sua organização ou sites do SharePoint mais populares de saudação.
- Monitorar alterações de configuração do administrador atividades tootrack ou operações de alto privilégio.
- Detecte e investigue comportamento indesejado do usuário, o que pode ser personalizado para suas necessidades organizacionais.
- Demonstre auditoria e conformidade. Por exemplo, você pode monitorar as operações de acesso de arquivos em arquivos confidenciais, que podem ajudá-lo com o processo de conformidade e auditoria hello.
- Execute a solução de problemas operacionais usando a Pesquisa do OMS sobre os dados de atividade do Office 365 da sua organização.

## <a name="prerequisites"></a>Pré-requisitos
seguinte Olá é necessário toothis anterior solução que está sendo instalado e configurado.

- Assinatura organizacional do Office 365.
- Credenciais para uma conta de usuário que seja um Administrador Global.
- dados de auditoria tooreceive, você deve [Configurar auditoria](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) na sua assinatura do Office 365.  Observe que a [auditoria de caixa de correio](https://technet.microsoft.com/library/dn879651.aspx) é configurada separadamente.  Você ainda pode instalar solução hello e coletar outros dados se a auditoria não está configurada.
 


## <a name="management-packs"></a>Pacotes de gerenciamento
Essa solução não instala nenhum pacote de gerenciamento nos grupos de gerenciamento conectados.
  

## <a name="configuration"></a>Configuração
Depois que você [Adicionar assinatura do Office 365 de saudação solução tooyour](../log-analytics/log-analytics-add-solutions.md), você tem tooconnect-tooyour assinatura do Office 365.

1. Adicionar tooyour de solução de gerenciamento de alertas Olá espaço de trabalho do OMS usando Olá processo descrito em [adicionar soluções](../log-analytics/log-analytics-add-solutions.md).
2. Vá muito**configurações** no portal do OMS hello.
3. Em **Fontes Conectadas**, selecione **Office 365**.
4. Clique em **Conectar o Office 365**.<br>![Conectar o Office 365](media/oms-solution-office-365/configure.png)
5. Entrar tooOffice 365 com uma conta que seja um Administrador Global para sua assinatura. 
6. assinatura de saudação será listada com cargas de trabalho Olá solução Olá monitorará.<br>![Conectar o Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Coleta de dados
### <a name="supported-agents"></a>Agentes com suporte
Olá solução do Office 365 não recupera os dados de qualquer um dos Olá [agentes do OMS](../log-analytics/log-analytics-data-sources.md).  Ela recupera dados diretamente do Office 365.

### <a name="collection-frequency"></a>Frequência de coleta
O Office 365 envia um [webhook notificação](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) com dados detalhados tooLog análise cada vez que um registro é criado.

## <a name="using-hello-solution"></a>Usando a solução de saudação
Quando você adiciona o espaço de trabalho do Office 365 de saudação solução tooyour OMS, Olá **Office 365** bloco será adicionado tooyour painel do OMS. Este bloco exibe uma contagem e a representação gráfica do número de saudação de computadores em seu ambiente e sua conformidade de atualização.<br><br>
![Bloco de Resumo do Office 365](media/oms-solution-office-365/tile.png)  

Clique em Olá **Office 365** bloco tooopen Olá **Office 365** painel.

![Painel do Office 365](media/oms-solution-office-365/dashboard.png)  

Painel de saudação inclui colunas de saudação de Olá a tabela a seguir. Cada coluna lista Olá superior dez alertas por meio da correspondência de contagem critérios da coluna para Olá especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que fornece toda a lista de saudação clicando consulte tudo na parte inferior de saudação da coluna de saudação ou clicando o cabeçalho da coluna hello.

| Coluna | Descrição |
|:--|:--|
| Operações | Fornece informações sobre Olá usuários ativos da sua monitorados todas as assinaturas do Office 365. Você também será capaz de toosee número de saudação de atividades que ocorrem ao longo do tempo.
| Exchange | Mostra a divisão de saudação de atividades do servidor do Exchange, como permissão de adicionar caixa de correio ou Set-Mailbox. |
| SharePoint | Mostra atividades principais Olá que os usuários façam em documentos do SharePoint. Quando você fazer drill down desse bloco, página de pesquisa de saudação mostra detalhes de saudação dessas atividades, como o documento de destino hello e local Olá dessa atividade. Por exemplo, para um evento de acessar o arquivo, você será capaz de toosee Olá documento que está sendo acessado, seu nome de conta associada e o endereço IP. |
| Azure Active Directory | Inclui as principais atividades do usuário, como Tentativas de Logon e de Redefinição de Senha do Usuário. Quando você fazer drill down, será capaz de toosee detalhes de Olá dessas atividades como Olá Status do resultado. Isso é mais útil se você quiser atividades suspeitas toomonitor no Active Directory do Azure. |




## <a name="log-analytics-records"></a>Registros do Log Analytics

Todos os registros criados no espaço de trabalho de análise de Log Olá pela solução Olá Office 365 têm um **tipo** de **OfficeActivity**.  Olá **OfficeWorkload** propriedade determina qual registro de saudação do serviço Office 365 refere-se muito Exchange, AzureActiveDirectory, SharePoint ou OneDrive.  Olá **RecordType** propriedade especifica o tipo de saudação da operação.  Propriedades de saudação variam para cada tipo de operação e são mostradas nas tabelas de saudação abaixo.

### <a name="common-properties"></a>Propriedades comuns
Olá propriedades a seguir é comuns registros de tooall Office 365.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo | *OfficeActivity* |
| ClientIP | endereço IP de saudação do dispositivo de saudação que foi usado quando hello atividade tenha sido registrada. endereço IP de saudação é exibido no formato de endereço de um IPv4 ou IPv6. |
| OfficeWorkload | Serviço Office 365 Olá registro se refere.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| Operação | nome de saudação de atividade do usuário ou administrador hello.  |
| OrganizationId | Olá GUID de locatário do Office 365 da sua organização. Esse valor será sempre ser hello mesmo para sua organização, independentemente do serviço Olá Office 365 no qual ele ocorre. |
| RecordType | Tipo de operação executada. |
| ResultStatus | Indica se a ação de hello (Olá especificado na propriedade Operation) foi bem-sucedida ou não. Os valores possíveis são Succeeded, PartiallySucceded ou Failed. Para a atividade de administração do Exchange, o valor de saudação é True ou False. |
| UserId | Olá UPN (Nome Principal do usuário) do usuário de saudação que realizou a ação Olá que resultaram em registro hello está sendo registrada em log. Por exemplo, my_name@my_domain_name. Observe que os registros para a atividade realizada por contas do sistema (como SHAREPOINT\system ou NTAUTHORITY\SYSTEM) também são incluídos. | 
| UserKey | Uma ID alternativa para o usuário Olá identificado no hello propriedade UserId.  Por exemplo, essa propriedade é preenchida com o ID exclusivo do hello passport (PUID) para eventos executados por usuários no SharePoint, o OneDrive for Business e Exchange. Essa propriedade também pode especificar Olá mesmo valor de propriedade UserID para eventos que ocorrem em outros serviços e eventos de saudação executado por contas do sistema|
| UserType | tipo de saudação do usuário que executou a operação de saudação.<br><br>Administrador<br>Aplicativo<br>DcAdmin<br>Regular <br>Reservado<br>ServicePrincipal<br>Sistema |


### <a name="azure-active-directory-base"></a>Base do Azure Active Directory
Olá propriedades a seguir é registros de Active Directory do Azure tooall comuns.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | tipo de saudação do evento do AD do Azure. |
| ExtendedProperties | Olá propriedades estendidas de evento de saudação do AD do Azure. |


### <a name="azure-active-directory-account-logon"></a>Logon na Conta do Azure Active Directory
Esses registros são criados quando um usuário do Active Directory tenta toolog em.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| Aplicativo | aplicativo Hello que dispara o evento de logon de conta de saudação, como Office 15. |
| Cliente | Detalhes sobre o cliente Olá dispositivo, o SO do dispositivo e o navegador de dispositivo que foi usado para saudação do evento de logon de conta de saudação. |
| LoginStatus | Esta propriedade é diretamente de OrgIdLogon.LoginStatus. mapeamento de saudação vários interessantes de falhas de logon pode ser feito por algoritmos de alerta. |
| UserDomain | Olá informações de identidade do locatário (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Esses registros são criados ao fazer alterações ou adições tooAzure objetos do Active Directory.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | usuário Olá Olá (identificada pela propriedade de operação de saudação) de ação foi executado em. |
| Ator | usuário de saudação ou entidade de serviço que executou a ação de saudação. |
| ActorContextId | Olá GUID da organização Olá Olá ator pertence. |
| ActorIpAddress | Olá endereço IP do ator no formato de endereço IPV4 ou IPV6. |
| InterSystemsId | Olá GUID que controlam ações Olá em componentes no serviço Olá Office 365. |
| IntraSystemId |   Olá GUID gerado pela ação de saudação do Active Directory do Azure tootrack. |
| SupportTicketId | Prezado cliente oferece suporte a ID do ticket para ação hello "agir em nome de" situações. |
| TargetContextId | Olá GUID da organização Olá Olá determinado usuário pertence. |


### <a name="data-center-security"></a>Segurança do Data Center
Esses registros são criados de dados de auditoria de Segurança do Data Center.  

| Propriedade | Descrição |
|:--- |:--- |
| EffectiveOrganization | nome de saudação do locatário Olá Olá elevação/cmdlet foi direcionado. |
| ElevationApprovedTime | Olá carimbo de hora de quando elevação Olá foi aprovada. |
| ElevationApprover | nome de saudação de um Gerenciador de Microsoft. |
| ElevationDuration | duração de saudação para qual Olá elevação estava ativa. |
| ElevationRequestId |  Um identificador exclusivo para a solicitação de elevação hello. |
| ElevationRole | elevação de saudação do função Hello foi solicitada para. |
| ElevationTime | Olá hora de início da elevação de saudação. |
| Start_Time | Olá hora de início da execução do cmdlet hello. |


### <a name="exchange-admin"></a>Exchange Admin
Esses registros são criados quando as alterações são feitas tooExchange configuração.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  Especifica se o cmdlet Olá foi executado por um usuário em sua organização, pela equipe do Microsoft datacenter ou uma conta de serviço do datacenter ou por um administrador delegado. valor Olá False indica que esse cmdlet Olá foi executado por alguém de sua organização. valor de Olá True indica que esse cmdlet Olá foi executado pela equipe do data center, uma conta de serviço do datacenter ou um administrador delegado. |
| ModifiedObjectResolvedName |  Este é o nome amigável de usuário de saudação do objeto Olá que foi modificado por Olá cmdlet. Isso é registrado somente se Olá cmdlet modifica o objeto hello. |
| OrganizationName | nome de saudação do locatário de saudação. |
| OriginatingServer | Olá o nome do servidor de saudação do qual Olá cmdlet foi executado. |
| parâmetros | nome de saudação e o valor para todos os parâmetros que foram usados com o cmdlet Olá identificado no hello propriedade de operações. |


### <a name="exchange-mailbox"></a>Caixa de correio do Exchange
Esses registros são criados quando as alterações ou adições são feitas tooExchange caixas de correio.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | Informações sobre o cliente de email de saudação que foi usado tooperform Olá operação, como uma versão do navegador, versão do Outlook e informações do dispositivo móvel. |
| Client_IPAddress | endereço IP de saudação do dispositivo de saudação que foi usado quando a operação de saudação foi registrada. endereço IP de saudação é exibido no formato de endereço de um IPv4 ou IPv6. |
| ClientMachineName | nome da máquina Olá que hospeda o cliente do Outlook hello. |
| ClientProcessName | cliente de email do Hello que foi a caixa de correio de saudação tooaccess usado. |
| ClientVersion | versão de saudação do cliente de email hello. |
| InternalLogonType | Reservado para uso interno. |
| Logon_Type | Indica o tipo de saudação do usuário acessada da caixa de correio hello e executou Olá operação que foi registrada. |
| LogonUserDisplayName |    nome amigável de saudação do usuário Olá que realizou a operação de saudação. |
| LogonUserSid | Olá SID de usuário de saudação que realizou a operação de saudação. |
| MailboxGuid | Olá GUID do Exchange da caixa de correio de saudação que foi acessada. |
| MailboxOwnerMasterAccountSid | O SID da conta mestre da conta do proprietário da caixa de correio. |
| MailboxOwnerSid | Olá SID do proprietário da caixa de correio de saudação. |
| MailboxOwnerUPN | endereço de email de saudação do hello quem possui a caixa de correio de saudação que foi acessada. |


### <a name="exchange-mailbox-audit"></a>Auditoria de Caixa de Correio do Exchange
Esses registros são criados quando é criada uma entrada de auditoria de caixa de correio.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| Item | Representa o item Olá após a qual Olá a operação foi executada | 
| SendAsUserMailboxGuid | Olá GUID do Exchange da caixa de correio de saudação que foi acessado toosend email como. |
| SendAsUserSmtp | Endereço SMTP do usuário de saudação que está sendo representado. |
| SendonBehalfOfUserMailboxGuid | Olá GUID do Exchange da caixa de correio de saudação que foi acessado toosend emails em nome de. |
| SendOnBehalfOfUserSmtp | Endereço SMTP do usuário de saudação em cujo nome hello email é enviado. |


### <a name="exchange-mailbox-audit-group"></a>Grupo de Auditoria da Caixa de Correio do Exchange
Esses registros são criados quando as alterações ou adições são feitas tooExchange grupos.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Informações sobre cada item no grupo de saudação. |
| CrossMailboxOperations | Indica se a operação de saudação envolvido mais de uma caixa de correio. |
| DestMailboxId | Definido somente se Olá CrossMailboxOperations parâmetro for True. Especifica o GUID de correio de destino hello. |
| DestMailboxOwnerMasterAccountSid | Definido somente se Olá CrossMailboxOperations parâmetro for True. Especifica o hello SID para Olá mestre a SID da conta de proprietário de caixa de correio de destino hello. |
| DestMailboxOwnerSid | Definido somente se Olá CrossMailboxOperations parâmetro for True. Especifica a saudação SID da caixa de correio de destino de saudação. |
| DestMailboxOwnerUPN | Definido somente se Olá CrossMailboxOperations parâmetro for True. Especifica a saudação UPN de proprietário de saudação da caixa de correio de destino de saudação. |
| DestFolder | pasta de destino Olá para operações como mover. |
| Pasta | Olá pasta onde se encontra um grupo de itens. |
| Pastas |     Informações sobre pastas de origem Olá envolvidas em uma operação; Por exemplo, se as pastas estão selecionadas e, em seguida, são excluídas. |


### <a name="sharepoint-base"></a>Base do SharePoint
Essas propriedades são registros de SharePoint tooall comuns.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Identifica o que ocorreu um evento no SharePoint. Os valores possíveis são SharePoint ou ObjectModel. |
| ItemType | tipo de saudação do objeto que foi acessado ou modificado. Consulte tabela de ItemType Olá para obter detalhes sobre os tipos de saudação de objetos. |
| MachineDomainInfo | Obter informações sobre operações de sincronização do dispositivo. Essas informações só serão informadas se ele estiver presente na solicitação de saudação. |
| MachineId |   Obter informações sobre operações de sincronização do dispositivo. Essas informações só serão informadas se ele estiver presente na solicitação de saudação. |
| Site_ | Olá GUID do site Olá onde arquivo hello ou pasta acessados pelo usuário hello está localizada. |
| Source_Name | entidade Olá que disparou Olá auditada operação. Os valores possíveis são SharePoint ou ObjectModel. |
| UserAgent | Informações sobre o cliente ou o navegador do usuário hello. Essas informações são fornecidas pelo cliente hello ou um navegador. |


### <a name="sharepoint-schema"></a>Esquema do SharePoint
Esses registros são criados quando alterações são efetuadas tooSharePoint.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Cadeia de caracteres opcional para eventos personalizados. |
| Event_Data |  Conteúdo opcional para eventos personalizados. |
| ModifiedProperties | propriedade Olá é incluída para os eventos admin, como adicionar um usuário como um membro de um site ou um grupo de administração do conjunto de sites. propriedade Olá inclui nome de saudação da propriedade Olá que foi modificada (por exemplo, grupo de administração de Site Olá), Olá novo valor de saudação modificou a propriedade (tal usuário Olá que foi adicionado como um administrador do site) e valor anterior Olá Olá modificou o objeto. |


### <a name="sharepoint-file-operations"></a>Operações de arquivo do SharePoint
Esses registros são criados em operações de toofile de resposta no SharePoint.

| Propriedade | Descrição |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | extensão de arquivo Hello de um arquivo que é copiado ou movido. Essa propriedade é exibida apenas para eventos FileCopied e FileMoved. |
| DestinationFileName | nome de saudação do arquivo de saudação que é copiado ou movido. Essa propriedade é exibida apenas para eventos FileCopied e FileMoved. |
| DestinationRelativeUrl | Olá URL da pasta de destino Olá onde um arquivo é copiado ou movido. Olá combinações de saudação valores para parâmetros SiteURL, DestinationRelativeURL e DestinationFileName é Olá igual ao valor de saudação para a propriedade de ObjectID hello, que é o nome de caminho completo Olá para o arquivo hello que foi copiado. Essa propriedade é exibida apenas para eventos FileCopied e FileMoved. |
| SharingType | tipo de saudação do que foram atribuídas a usuários toohello que Olá recurso foi compartilhado com permissões de compartilhamento. Esse usuário é identificado pelo parâmetro de UserSharedWith hello. |
| Site_Url | Olá o URL do site de saudação onde arquivo hello ou pasta acessados pelo usuário hello está localizada. |
| SourceFileExtension | extensão de arquivo de saudação do arquivo hello acessada pelo usuário hello. Esta propriedade é em branco se o objeto de saudação que foi acessado é uma pasta. |
| SourceFileName |  nome de saudação do arquivo hello ou pasta acessados pelo usuário hello. |
| SourceRelativeUrl | Olá o URL da pasta de saudação que contém o arquivo hello acessado pelo usuário hello. Olá combinações de saudação valores para parâmetros de SiteURL, SourceRelativeURL e SourceFileName Olá é Olá igual ao valor de saudação para a propriedade de ObjectID hello, que é o nome do caminho completo Olá para o arquivo hello acessado pelo usuário Olá. |
| UserSharedWith |  usuário de saudação que um recurso foi compartilhado com. |




## <a name="sample-log-searches"></a>Pesquisas de log de exemplo
Olá, a tabela a seguir fornece as pesquisas de log de exemplo para atualizar registros coletados por essa solução.

| Consultar | Descrição |
| --- | --- |
|Contagem de todas as operações de saudação de sua assinatura do Office 365 |`Type = OfficeActivity | measure count() by Operation` |
|Uso de sites do SharePoint|`Type=OfficeActivity OfficeWorkload=sharepoint | measure count() as Count by SiteUrl | sort Count asc`|
|Operações de acesso de arquivos por tipo de usuário|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|Pesquisar com uma palavra-chave específica|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Monitorar de ações externas no Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Solucionar problemas

Se sua solução do Office 365 não está coletando dados conforme o esperado, verifique seu status no portal do OMS Olá em **configurações** -> **fontes conectadas** -> **Office 365** . Olá, a tabela a seguir descreve cada status.

| Status | Descrição |
|:--|:--|
| Ativo | saudação de assinatura do Office 365 está ativa e carga de trabalho de saudação é o espaço de trabalho OMS tooyour conectado com êxito. |
| Pendente | saudação de assinatura do Office 365 está ativa, mas cargas de trabalho Olá não ainda tiver sido conectado tooyour espaço de trabalho do OMS com êxito. Olá primeira vez que você se conectar a assinatura Olá Office 365, todas as cargas de trabalho Olá será esse status até que eles estão conectados com êxito. Aguarde 24 horas para todos os Olá cargas de trabalho tooswitch tooActive. |
| Inativo | saudação de assinatura do Office 365 está em um estado inativo. Consulte a página de Administração do Office 365 para obter detalhes. Depois de ativar sua assinatura do Office 365, desvincule-lo do seu espaço de trabalho do OMS e vinculá-lo novamente toostart recebendo dados. |



## <a name="next-steps"></a>Próximas etapas
* Usar pesquisas de Log no [análise de Log](../log-analytics/log-analytics-log-searches.md) tooview detalhadas de atualização de dados.
* [Criar seus próprios painéis](../log-analytics/log-analytics-dashboards.md) toodisplay suas consultas de pesquisa favoritas do Office 365.
* [Criar alertas](../log-analytics/log-analytics-alerts.md) toobe proativamente notificado das atividades importantes do Office 365.  
