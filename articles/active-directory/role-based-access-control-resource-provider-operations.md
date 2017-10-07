---
title: "Operações de provedor do Gerenciador de recursos de aaaAzure | Microsoft Docs"
description: "Detalhes Olá operações disponíveis nos provedores de recursos do Gerenciador de recursos do Microsoft Azure Olá"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Operações do provedor de recursos do Azure Resource Manager

Este documento lista operações Olá disponíveis para cada provedor de recursos do Gerenciador de recursos do Microsoft Azure. Eles podem ser usados em funções personalizadas tooprovide granular controle de acesso baseado em função (RBAC) permissões tooresources no Azure. Observe que esta não é uma lista abrangente e outras operações podem ser adicionadas ou removidas conforme a atualização de cada provedor. Cadeias de caracteres de operação seguem o formato de saudação do `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Para obter uma lista abrangente e atual use `Get-AzureRmProviderOperation` (no PowerShell) ou `azure provider operations show` (no Azure CLI) operações toolist de provedores de recursos do Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Operação | Descrição |
|---|---|
|/configuration/action|Atualizar a configuração do locatário.|
|/services/action|Atualiza uma instância de serviço no locatário hello.|
|/configuration/write|Criar uma configuração de locatário.|
|/configuration/read|Lê Olá configuração de locatário.|
|/services/write|Cria uma instância de serviço no locatário hello.|
|/services/read|Lê as instâncias de serviço Olá no locatário hello.|
|/services/delete|Exclui uma instância de serviço no locatário hello.|
|/services/servicemembers/action|Cria uma instância de membro de serviço no serviço de saudação.|
|/services/servicemembers/read|Lê a instância do membro Olá serviço no serviço de saudação.|
|/services/servicemembers/delete|Exclui uma instância de membro de serviço no serviço de saudação.|
|/services/servicemembers/alerts/read|Lê os alertas de saudação para um membro do serviço.|
|/services/alerts/read|Lê os alertas de saudação para um serviço.|
|/services/alerts/read|Lê os alertas de saudação para um serviço.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Operação | Descrição |
|---|---|
|/generateRecommendations/action|Gera recomendações|
|/suppressions/action|Criar/atualizar supressões|
|/register/action|Registra a assinatura Olá Olá Microsoft Advisor|
|/generateRecommendations/read|Obter o status de gerar recomendações|
|/recommendations/read|Ler recomendações|
|/suppressions/read|Obter supressões|
|/suppressions/delete|Excluir supressão|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Operação | Descrição |
|---|---|
|/servers/read|Recupera as informações sobre a saudação de saudação especificado Analysis Server.|
|/servers/write|Cria ou atualiza Olá especificado Analysis Server.|
|/servers/delete|Exclusões Olá Analysis Server.|
|/servers/suspend/action|Suspende Olá Analysis Server.|
|/servers/resume/action|Retoma hello Analysis Server.|
|/servers/checkNameAvailability<br>/action|Verificar se determinado nome do Analysis Server é válido e não está em uso.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Operação | Descrição |
|---|---|
|/checkNameAvailability/action|Verificar se o nome do serviço fornecido está disponível|
|/register/action|Registrar a assinatura para o provedor de recursos Microsoft.ApiManagement|
|/unregister/action|Cancelar o registro da assinatura para o provedor de recursos Microsoft.ApiManagement|
|/service/write|Criar uma nova instância do Serviço de Gerenciamento de API|
|/service/read|Ler metadados de uma instância do Serviço de Gerenciamento de API|
|/service/delete|Excluir uma instância do Serviço de Gerenciamento de API|
|/service/updatehostname/action|Configurar, atualizar ou remover nomes de domínio personalizado para um Serviço de Gerenciamento de API|
|/service/uploadcertificate/action|Carregar certificado SSL para um Serviço de Gerenciamento de API|
|/service/backup/action|Contêiner especificado do backup toohello de serviço de gerenciamento de API em um usuário forneceu a conta de armazenamento|
|/service/restore/action|Restaurar o serviço de gerenciamento de API do contêiner de saudação especificado em um conta de armazenamento de fornecida pelo usuário|
|/service/managedeployments/action|Alterar SKU/unidades, adicionar/remover implantações regionais do Serviço de Gerenciamento de API|
|/service/getssotoken/action|Obtém o token SSO que pode ser usado toologin no portal herdado de serviço de gerenciamento de API como um administrador|
|/service/applynetworkconfigurationupdates/action|Atualizações Olá Microsoft.ApiManagement recursos em execução na rede Virtual toopick atualizadas as configurações de rede.|
|/service/operationresults/read|Obter o status atual da operação de longa duração|
|/service/networkStatus/read|Obtém o status de acesso de rede de saudação de recursos.|
|/service/loggers/read|Obter lista de agentes ou obter detalhes do agente|
|/service/loggers/write|Adicionar novo agente ou atualizar detalhes do agente existente|
|/service/loggers/delete|Remover agente existente|
|/service/users/read|Obter uma lista de usuários registrados ou obter detalhes da conta de um usuário|
|/service/users/write|Registrar um novo usuário ou atualizar detalhes da conta de um usuário existente|
|/service/users/delete|Remover conta de usuário|
|/service/users/generateSsoUrl/action|Gerar a URL do SSO. Olá URL pode ser usado tooaccess portal de administração|
|/service/users/subscriptions/read|Obter lista de assinaturas do usuário|
|/service/users/keys/read|Obter lista de chaves do usuário|
|/service/users/groups/read|Obter lista de grupos do usuário|
|/service/tenant/operationResults/read|Obter lista de resultados da operação ou obter o resultado de uma operação específica|
|/service/tenant/policy/read|Obter configuração de política para o locatário Olá|
|/service/tenant/policy/write|Configuração de política para o locatário Olá|
|/service/tenant/policy/delete|Remover configuração de política para o locatário Olá|
|/service/tenant/configuration/save/action|Cria confirmação com a ramificação específica de toohello do instantâneo de configuração no repositório de saudação|
|/service/tenant/configuration/deploy/action|Executa uma tarefa de implantação tooapply alterações de configuração de toohello de ramificação Olá git especificado no banco de dados.|
|/service/tenant/configuration/validate/action|Valida as alterações do branch de git especificado Olá|
|/service/tenant/configuration/operationResults/read|Obter lista de resultados da operação ou obter o resultado de uma operação específica|
|/service/tenant/configuration/syncState/read|Obter status da última sincronização git|
|/service/tenant/access/read|Obter informações detalhadas de acesso do locatário|
|/service/tenant/access/write|Atualizar os detalhes de informações de acesso do locatário|
|/service/tenant/access/regeneratePrimaryKey/action|Regenerar a chave de acesso primária|
|/service/tenant/access/regenerateSecondaryKey/action|Regenerar a chave de acesso secundária|
|/service/identityProviders/read|Obter lista de provedores de identidade ou obter detalhes do provedor de identidade|
|/service/identityProviders/write|Criar um novo provedor de identidade atualizar detalhes de um provedor de identidade existente|
|/service/identityProviders/delete|Remover o provedor de identidade existente|
|/service/subscriptions/read|Obter uma lista de assinaturas de produtos ou obter os detalhes de assinatura do produto|
|/service/subscriptions/write|Inscrever-se um produto existente do usuário tooan existente ou atualizar os detalhes da assinatura existente. Essa operação pode ser usado toorenew assinatura|
|/service/subscriptions/delete|Excluir assinatura. Essa operação pode ser usado toodelete assinatura|
|/service/subscriptions/regeneratePrimaryKey/action|Regenerar a chave primária da assinatura|
|/service/subscriptions/regenerateSecondaryKey/action|Regenerar a chave secundária da assinatura|
|/service/backends/read|Obter lista de back-ends ou obter os detalhes de back-end|
|/service/backends/write|Adicionar um novo back-end ou atualizar os detalhes do back-end existente|
|/service/backends/delete|Remover o back-end existente|
|/service/apis/read|Obter lista de todas as APIs registradas ou obter detalhes da API|
|/service/apis/write|Criar nova API ou atualizar os detalhes da API existente|
|/service/apis/delete|Remover a API existente|
|/service/apis/policy/read|Obter detalhes de configuração de política para API|
|/service/apis/policy/write|Definir detalhes de configuração de política para API|
|/service/apis/policy/delete|Remover configuração de política da API|
|/service/apis/operations/read|Obter lista de operações de API existentes ou obter os detalhes de operação da API|
|/service/apis/operations/write|Criar nova operação de API ou atualizar operação de API existente|
|/service/apis/operations/delete|Remover a operação da API existente|
|/service/apis/operations/policy/read|Obter detalhes de configuração de política para a operação|
|/service/apis/operations/policy/write|Definir detalhes de configuração de política para a operação|
|/service/apis/operations/policy/delete|Remover configuração de política da operação|
|/service/products/read|Obter lista de produtos ou obter detalhes do produto|
|/service/products/write|Criar novo produto ou atualizar detalhes do produto existente|
|/service/products/delete|Remover produto existente|
|/service/products/subscriptions/read|Obter lista de assinaturas de produto|
|/service/products/apis/read|Obter uma lista de APIs adicionado tooexisting produto|
|/service/products/apis/write|Adicionar um produto de tooexisting API existente|
|/service/products/apis/delete|Remover API existente do produto existente|
|/service/products/policy/read|Obter a configuração de política do produto existente|
|/service/products/policy/write|Definir a configuração de política para o produto existente|
|/service/products/policy/delete|Remover configuração de política de produto existente|
|/service/products/groups/read|Obter lista de grupos de desenvolvedores associados ao produto|
|/service/products/groups/write|Associar o grupo do desenvolvedor existente ao produto existente|
|/service/products/groups/delete|Excluir a associação de grupo do desenvolvedor existente ao produto existente|
|/service/openidConnectProviders/read|Obter lista de provedores OpenID Connect ou obter detalhes do provedor OpenID Connect|
|/service/openidConnectProviders/write|Criar um novo provedor OpenID Connect ou atualizar detalhes de um provedor OpenID Connect existente|
|/service/openidConnectProviders/delete|Remover o provedor OpenID Connect existente|
|/service/certificates/read|Obter lista de certificados ou obter os detalhes do certificado|
|/service/certificates/write|Adicionar novo certificado|
|/service/certificates/delete|Remover certificado existente|
|/service/properties/read|Obter a lista de todas as propriedades ou obtém detalhes de uma propriedade especificada|
|/service/properties/write|Criar uma nova propriedade ou atualizar o valor da propriedade especificada|
|/service/properties/delete|Remover uma propriedade existente|
|/service/groups/read|Obter lista de grupos ou obter detalhes de um grupo|
|/service/groups/write|Criar novo grupo ou atualizar detalhes do grupo existente|
|/service/groups/delete|Remover grupo existente|
|/service/groups/users/read|Obter lista de usuários do grupo|
|/service/groups/users/write|Adicionar grupo de tooexisting de usuário existente|
|/service/groups/users/delete|Remover usuário existente do grupo existente|
|/service/authorizationServers/read|Obter lista de servidores de autorização ou obter detalhes do servidor de autorização|
|/service/authorizationServers/write|Criar um novo servidor de autorização ou atualizar detalhes de um servidor de autorização existente|
|/service/authorizationServers/delete|Remover servidor de autorização existente|
|/service/reports/bySubscription/read|Obter relatórios agregados por assinatura.|
|/service/reports/byRequest/read|Obter solicitações de dados de relatório|
|/service/reports/byOperation/read|Obter relatórios agregados por operações|
|/service/reports/byGeo/read|Obter relatórios agregados por região geográfica|
|/service/reports/byUser/read|Obter relatórios agregados por desenvolvedores.|
|/service/reports/byTime/read|Obter relatórios agregados por intervalos de tempo|
|/service/reports/byApi/read|Obter relatórios agregados por APIs|
|/service/reports/byProduct/read|Obter relatórios agregados por produtos.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Operação | Descrição |
|---|---|
|/appidentities/Read|Retorna Olá recursos (site da web) registrado com hello Gateway.|
|/appidentities/Write|Criar uma nova identidade de aplicativo.|
|/appidentities/Delete|Excluir uma identidade de aplicativo existente.|
|/deploymenttemplates/listMetadata/Action|Lista os metadados de interface do usuário associados Olá pacote API App.|
|/deploymenttemplates/generate/Action|Retorna um modelo de implantação de tooprovision API App instância (s).|
|/gateways/Read|Instância do Gateway Olá retorna.|
|/gateways/Write|Criar um novo Gateway ou atualizar um existente.|
|/gateways/Delete|Excluir uma instância do Gateway existente.|
|/gateways/listLoginUris/Action|Preenche o repositório de token e retorna URIs de login OAuth.|
|/gateways/listKeys/Action|Retornar os segredos de gateway.|
|/gateways/tokens/Write|Cria um novo Zumo Token com nome hello.|
|/gateways/registrations/Read|Retorna Olá recursos (site da web) registrado com hello Gateway.|
|/gateways/registrations/Write|Registra um recurso (site da web) com hello Gateway.|
|/gateways/registrations/Delete|Cancela o registro de um recurso (site da web) do hello Gateway.|
|/apiapps/Read|Retorna Olá instância API App.|
|/apiapps/Write|Criar um novo aplicativo de API ou atualizar um existente.|
|/apiapps/Delete|Excluir uma instância existente do aplicativo de API.|
|/apiapps/listStatus/Action|Retornar o status do aplicativo de API.|
|/apiapps/listKeys/Action|Retornar segredos do aplicativo de API.|
|/apiapps/apidefinitions/Read|Retornar a definição de API do aplicativo de API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Operação | Descrição |
|---|---|
|/elevateAccess/action|Olá de concede acesso de administrador de acesso do usuário no escopo de locatário de saudação do chamador|
|/classicAdministrators/read|Lê administradores Olá para assinatura de saudação.|
|/classicAdministrators/write|Adicionar ou modificar administrador tooa assinatura.|
|/classicAdministrators/delete|Remove o administrador de saudação da assinatura hello.|
|/locks/read|Obtém bloqueios no hello especificado escopo.|
|bloqueios/gravação|Adicionar bloqueios no hello especificado escopo.|
|/locks/delete|Excluir bloqueios no hello especificado escopo.|
|/policyAssignments/read|Obter informações sobre uma atribuição de política.|
|/policyAssignments/write|Criar uma política de atribuição no hello especificado escopo.|
|/policyAssignments/delete|Excluir uma atribuição de política no hello especificado escopo.|
|/permissions/read|Lista todas as permissões de saudação chamador Olá tem em um determinado escopo.|
|/roleDefinitions/read|Obter informações sobre uma definição de função.|
|/roleDefinitions/write|Criar ou atualizar uma definição de função personalizada com permissões especificadas e escopos atribuíveis.|
|/roleDefinitions/delete|Excluir Olá especificado a definição de função personalizada.|
|/providerOperations/read|Obter operações para todos os provedores de recursos que podem ser usados em definições de função.|
|/policyDefinitions/read|Obter informações sobre uma definição de política.|
|/policyDefinitions/write|Criar uma definição de política personalizada.|
|/policyDefinitions/delete|Excluir uma definição de política.|
|/roleAssignments/read|Obter informações sobre uma atribuição de função.|
|/roleAssignments/write|Criar uma função de atribuição no hello especificado escopo.|
|/roleAssignments/delete|Excluir uma atribuição de função em Olá especificado escopo.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Operação | Descrição |
|---|---|
|/automationAccounts/read|Obter uma conta da Automação do Azure|
|/automationAccounts/write|Criar ou atualizar uma conta da Automação do Azure|
|/automationAccounts/delete|Excluir uma conta da Automação do Azure|
|/automationAccounts/configurations/readContent/action|Obter o conteúdo de DSC de Automação do Azure|
|/automationAccounts/hybridRunbookWorkerGroups/read|Ler recursos do Hybrid Runbook Worker|
|/automationAccounts/hybridRunbookWorkerGroups/delete|Excluir recursos do Hybrid Runbook Worker|
|/automationAccounts/jobSchedules/read|Obter uma agenda de trabalho da Automação do Azure|
|/automationAccounts/jobSchedules/write|Criar uma agenda de trabalho da Automação do Azure|
|/automationAccounts/jobSchedules/delete|Excluir uma agenda de trabalho da Automação do Azure|
|/automationAccounts/connectionTypes/read|Obter um ativo de tipo de conexão da Automação do Azure|
|/automationAccounts/connectionTypes/Write|Criar um ativo de tipo de conexão da Automação do Azure|
|/automationAccounts/connectionTypes/delete|Excluir um ativo de tipo de conexão da Automação do Azure|
|/automationAccounts/modules/read|Obter um módulo da Automação do Azure|
|/automationAccounts/modules/write|Criar ou atualizar um módulo da Automação do Azure|
|/automationAccounts/modules/delete|Excluir um módulo da Automação do Azure|
|/automationAccounts/credentials/read|Obter um ativo de credencial da Automação do Azure|
|/automationAccounts/credentials/write|Criar ou atualizar um ativo de credencial da Automação do Azure|
|/automationAccounts/credentials/delete|Excluir um ativo de credencial da Automação do Azure|
|/automationAccounts/certificates/read|Obter um ativo de certificado da Automação do Azure|
|/automationAccounts/certificates/write|Criar ou atualizar um ativo de certificado da Automação do Azure|
|/automationAccounts/certificates/delete|Excluir um ativo de certificado da Automação do Azure|
|/automationAccounts/schedules/read|Obter um ativo de agendamento da Automação do Azure|
|/automationAccounts/schedules/write|Criar ou atualizar um ativo de agendamento da Automação do Azure|
|/automationAccounts/schedules/delete|Excluir um ativo de agendamento da Automação do Azure|
|/automationAccounts/jobs/read|Obter um trabalho da Automação do Azure|
|/automationAccounts/jobs/write|Criar um trabalho da Automação do Azure|
|/automationAccounts/jobs/stop/action|Interrompe um trabalho da Automação do Azure|
|/automationAccounts/jobs/suspend/action|Suspende um trabalho da Automação do Azure|
|/automationAccounts/jobs/resume/action|Reinicia um trabalho da Automação do Azure|
|/automationAccounts/jobs/runbookContent/action|Obtém o conteúdo de saudação do runbook de automação do Azure Olá momento Olá Olá da execução do trabalho|
|/automationAccounts/jobs/output/action|Obtém a saída de saudação de um trabalho|
|/automationAccounts/jobs/read|Obter um trabalho da Automação do Azure|
|/automationAccounts/jobs/write|Criar um trabalho da Automação do Azure|
|/automationAccounts/jobs/stop/action|Interrompe um trabalho da Automação do Azure|
|/automationAccounts/jobs/suspend/action|Suspende um trabalho da Automação do Azure|
|/automationAccounts/jobs/resume/action|Reinicia um trabalho da Automação do Azure|
|/automationAccounts/jobs/streams/read|Obter um fluxo de trabalho da Automação do Azure|
|/automationAccounts/connections/read|Obter um ativo de conexão da Automação do Azure|
|/automationAccounts/connections/write|Criar ou atualizar um ativo de conexão da Automação do Azure|
|/automationAccounts/connections/delete|Excluir um ativo de conexão da Automação do Azure|
|/automationAccounts/variables/read|Ler um ativo de variável da Automação do Azure|
|/automationAccounts/variables/write|Criar ou atualizar um ativo de variável da Automação do Azure|
|/automationAccounts/variables/delete|Excluir um ativo de variável da Automação do Azure|
|/automationAccounts/runbooks/readContent/action|Obtém o conteúdo de saudação de um runbook de automação do Azure|
|/automationAccounts/runbooks/read|Obter um runbook da Automação do Azure|
|/automationAccounts/runbooks/write|Criar ou atualizar um runbook da Automação do Azure|
|/automationAccounts/runbooks/delete|Excluir um runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/readContent/action|Obtém o conteúdo de saudação de um rascunho de runbook de automação do Azure|
|/automationAccounts/runbooks/draft/writeContent/action|Cria o conteúdo de saudação de um rascunho de runbook de automação do Azure|
|/automationAccounts/runbooks/draft/read|Obter um rascunho de runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/publish/action|Publica um rascunho de runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/undoEdit/action|Desfazer edições tooan rascunho de runbook da automação do Azure|
|/automationAccounts/runbooks/draft/testJob/read|Obter um trabalho de teste de rascunho do runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/testJob/write|Criar um trabalho de teste de rascunho de runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/testJob/stop/action|Interrompe um trabalho de teste de rascunho de runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/testJob/suspend/action|Suspende um trabalho de teste de rascunho de runbook da Automação do Azure|
|/automationAccounts/runbooks/draft/testJob/resume/action|Retoma um trabalho de teste de rascunho de runbook da Automação do Azure|
|/automationAccounts/webhooks/read|Ler um webhook da Automação do Azure|
|/automationAccounts/webhooks/write|Criar ou atualizar um webhook da Automação do Azure|
|/automationAccounts/webhooks/delete|Excluir um webhook da Automação do Azure |
|/automationAccounts/webhooks/generateUri/action|Gera um URI para um webhook da Automação do Azure|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Esse provedor não é um provedor ARM completo e não fornece nenhuma operação de ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá Olá provedor de recursos de lote e permite a criação de saudação de contas em lotes|
|/batchAccounts/write|Criar uma nova conta do Lote ou atualizar uma conta do Lote existente|
|/batchAccounts/read|Lista de contas em lotes ou obtém as propriedades de saudação de uma conta de lote|
|/batchAccounts/delete|Excluir uma conta do Lote|
|/batchAccounts/listkeys/action|Listar chaves de acesso para uma conta do Lote|
|/batchAccounts/regeneratekeys/action|Regenera chaves de acesso para uma conta do Lote|
|/batchAccounts/syncAutoStorageKeys/action|Sincroniza as chaves de acesso para a conta de armazenamento auto Olá para uma conta de lote|
|/batchAccounts/applications/read|Lista os aplicativos ou obtém as propriedades de saudação de um aplicativo|
|/batchAccounts/applications/write|Criar um novo aplicativo ou atualizar um aplicativo existente|
|/batchAccounts/applications/delete|Excluir um aplicativo|
|/batchAccounts/applications/versions/read|Obtém as propriedades de saudação de um pacote de aplicativo|
|/batchAccounts/applications/versions/write|Criar um novo pacote de aplicativos ou atualizar um pacote de aplicativos existente|
|/batchAccounts/applications/versions/activate/action|Ativa um pacote de aplicativos|
|/batchAccounts/applications/versions/delete|Excluir um pacote de aplicativos|
|/locations/quotas/read|Obtém cotas de lote de saudação especificado assinatura na região do Azure especificada de saudação|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Operação | Descrição |
|---|---|
|/invoices/read|Listar faturas disponíveis|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Operação | Descrição |
|---|---|
|/mapApis/Read|Operação de Leitura|
|/mapApis/Write|Operação de Gravação|
|/mapApis/Delete|Operação de Exclusão|
|/mapApis/regenerateKey/action|Regenera Olá chave|
|/mapApis/listSecrets/action|Olá lista segredos|
|/mapApis/listSingleSignOnToken/action|Olá leitura único logon na autorização Token para recursos|
|/Operations/read|Descrição da operação de saudação.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Operação | Descrição |
|---|---|
|/checknameavailability/action|Verificar se um nome está disponível para uso com um novo Cache Redis|
|/register/action|Registra o provedor de recursos 'Microsoft.Cache' hello com uma assinatura|
|/unregister/action|Cancela o registro de provedor de recursos 'Microsoft.Cache' hello com uma assinatura|
|/redis/write|Modificar as configurações e a configuração no portal de gerenciamento Olá Olá Redis Cache|
|/redis/read|Exibir configurações e a configuração de saudação do Cache Redis no portal de gerenciamento de saudação|
|/redis/delete|Excluir Olá todo o Cache Redis|
|/redis/listKeys/action|Exibição Olá valor das chaves de acesso do Cache Redis no portal de gerenciamento Olá|
|/redis/regenerateKey/action|Alterar o valor de saudação das chaves de acesso do Cache Redis no portal de gerenciamento Olá|
|/redis/import/action|Importar dados em um formato especificado de vários blobs para o Redis|
|/redis/export/action|Exportar os blobs de armazenamento de tooprefixed Redis dados no formato especificado|
|/redis/forceReboot/action|Forçar a reinicialização de uma instância de cache, possivelmente com perda de dados.|
|/redis/stop/action|Interromper uma instância de cache.|
|/redis/start/action|Iniciar uma instância de cache.|
|/redis/metricDefinitions/read|Obtém métricas disponíveis Olá para um Cache Redis|
|/redis/firewallRules/read|Obter regras de firewall Olá IP de um Cache Redis|
|/redis/firewallRules/write|Editar regras de firewall Olá IP de um Cache Redis|
|/redis/firewallRules/delete|Excluir regras de firewall de IP de um Cache Redis|
|/redis/listUpgradeNotifications/read|Lista Olá notificações de atualização mais recente para o locatário de cache de saudação.|
|/redis/linkedservers/read|Obter servidores vinculados associados a um Cache Redis.|
|/redis/linkedservers/write|Adicionar um servidor vinculado tooa Cache Redis|
|/redis/linkedservers/delete|Excluir servidor vinculado de um Cache Redis|
|/redis/patchSchedules/read|Obtém o hello patches agenda de um Cache Redis|
|/redis/patchSchedules/write|Modificar Olá patches agenda de um Cache Redis|
|/redis/patchSchedules/delete|Excluir Olá patch agenda de um Cache Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Operação | Descrição |
|---|---|
|/provisionGlobalAppServicePrincipalInUserTenant/Action|Provisionar entidade de serviço para entidade de serviço de aplicativo|
|/validateCertificateRegistrationInformation/Action|Validar objeto de compra de certificado sem enviá-lo|
|/register/action|Registrar o provedor de recursos Microsoft Certificates Olá para assinatura de saudação|
|/certificateOrders/Write|Adicionar uma nova certificateOrder ou atualizar uma existente|
|/certificateOrders/Delete|Excluir um AppServiceCertificate existente|
|/certificateOrders/Read|Obter lista de saudação do CertificateOrders|
|/certificateOrders/reissue/Action|Emitir novamente um certificateorder existente|
|/certificateOrders/renew/Action|Renovar um certificateorder existente|
|/certificateOrders/retrieveCertificateActions/Action|Recuperar a lista de saudação de ações de certificado|
|/certificateOrders/retrieveEmailHistory/Action|Recuperar o histórico de email do certificado|
|/certificateOrders/resendEmail/Action|Reenviar email de certificado|
|/certificateOrders/verifyDomainOwnership/Action|Verificar a propriedade de domínio|
|/certificateOrders/resendRequestEmails/Action|Reenviar o endereço de email de tooanother de emails de solicitação|
|/certificateOrders/resendRequestEmails/Action|Recuperar o selo de site para um certificado do Serviço de Aplicativo emitido|
|/certificateOrders/certificates/Write|Adicionar um novo certificado ou atualizar um existente|
|/certificateOrders/certificates/Delete|Excluir um certificado existente|
|/certificateOrders/certificates/Read|Obter lista de saudação de certificados|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Operação | Descrição |
|---|---|
|/register/action|Registrar tooClassic computação|
|/checkDomainNameAvailability/action|Olá verifica a disponibilidade de um determinado nome de domínio.|
|/moveSubscriptionResources/action|Mova assinatura diferente do todos os recursos clássicos tooa.|
|/validateSubscriptionMoveAvailability/action|Valide a disponibilidade da assinatura Olá para operação de movimentação clássico.|
|/operatingSystemFamilies/read|Lista as famílias de sistema operacional convidado Olá disponíveis no Microsoft Azure e também lista as versões do sistema operacional Olá disponíveis para cada f
|/capabilities/read|Mostra os recursos de saudação|
|/operatingSystems/read|Lista Olá versões do sistema de operacional convidado Olá que estão atualmente disponíveis no Microsoft Azure.|
|/resourceTypes/skus/read|Obtém a lista de Sku de saudação para tipos de recursos com suporte.|
|/domainNames/read|Retorna os nomes de domínio Olá para recursos.|
|/domainNames/write|Adicionar ou modificar os nomes de domínio Olá para recursos.|
|/domainNames/delete|Remova os nomes de domínio Olá para recursos.|
|/domainNames/swap/action|Troca Olá slot de produção toohello slot de preparo.|
|/domainNames/serviceCertificates/read|Retorna Olá certificados de serviço usados.|
|/domainNames/serviceCertificates/write|Adicionar ou modificar os certificados de serviço Olá usados.|
|/domainNames/serviceCertificates/delete|Exclua certificados de serviço Olá usados.|
|/domainNames/serviceCertificates/operationStatuses/read|Lê o status da operação Olá para certificados de serviço de nomes de domínio hello.|
|/domainNames/capabilities/read|Mostra os recursos de nome de domínio Olá|
|/domainNames/extensions/read|Retorna Olá extensões de nome de domínio.|
|/domainNames/extensions/write|Adicione extensões de nome de domínio de saudação.|
|/domainNames/extensions/delete|Remova extensões de nome de domínio de saudação.|
|/domainNames/extensions/operationStatuses/read|Lê o status da operação Olá para extensões de nomes de domínio hello.|
|/domainNames/active/write|Define o nome de domínio do active hello.|
|/domainNames/slots/read|Mostra os slots de implantação hello.|
|/domainNames/slots/write|Cria ou atualiza a implantação de saudação.|
|/domainNames/slots/delete|Excluir determinado slot de implantação.|
|/domainNames/slots/start/action|Inicia um slot de implantação.|
|/domainNames/slots/stop/action|Suspende o slot de implantação de saudação.|
|/domainNames/slots/operationStatuses/read|Lê o status da operação Olá para slots de nomes de domínio hello.|
|/domainNames/slots/roles/read|Obter função hello slot de implantação de saudação.|
|/domainNames/slots/roles/extensionReferences/read|Retorna Olá referência de extensão de função do slot de implantação de saudação.|
|/domainNames/slots/roles/extensionReferences/write|Adicionar ou modificar a referência de extensão de saudação de função do slot de implantação de saudação.|
|/domainNames/slots/roles/extensionReferences/delete|Remova a referência de extensão de saudação de função do slot de implantação de saudação.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/read|Lê o status da operação de saudação de referências de extensão de funções de slots de nomes de domínio de saudação.|
|/domainNames/slots/roles/roleInstances/read|Obter a instância de função hello.|
|/domainNames/slots/roles/roleInstances/restart/action|Reinicia as instâncias de função.|
|/domainNames/slots/roles/roleInstances/reimage/action|Instância de função hello reimages.|
|/domainNames/slots/roles/roleInstances/operationStatuses/read|Lê o status da operação Olá para instâncias de função funções do slots de nomes de domínio hello.|
|/domainNames/slots/state/start/write|Alterações Olá toostopped de estado do slot de implantação.|
|/domainNames/slots/state/stop/write|Alterações Olá toostarted de estado do slot de implantação.|
|/domainNames/slots/upgradeDomain/write|Percorrer domínio de atualização hello.|
|/domainNames/internalLoadBalancers/read|Obtém os balanceadores de carga internos de saudação.|
|/domainNames/internalLoadBalancers/write|Criar um novo balanceamento de carga interno.|
|/domainNames/internalLoadBalancers/delete|Remover um novo balanceamento de carga interno.|
|/domainNames/internalLoadBalancers/operationStatuses/read|Lê o status da operação de saudação para nomes de domínio de saudação balanceadores de carga interno.|
|/domainNames/loadBalancedEndpointSets/read|Mostra os conjuntos de ponto de extremidade com balanceamento de carga Olá|
|/domainNames/loadBalancedEndpointSets/operationStatuses/read|Lê o status da operação de saudação para nomes de domínio de saudação conjuntos de ponto de extremidade com balanceamento de carga.|
|/domainNames/availabilitySets/read|Mostra Olá conjunto de disponibilidade para o recurso de saudação.|
|/quotas/read|Obter cota Olá Olá assinatura.|
|/virtualMachines/read|Retorna a lista de máquinas virtuais.|
|/virtualMachines/write|Adicionar ou modificar máquinas virtuais.|
|/virtualMachines/delete|Remover as máquinas virtuais.|
|/virtualMachines/start/action|Inicie a máquina virtual de saudação.|
|/virtualMachines/redeploy/action|Reimplantar a máquina virtual de saudação.|
|/virtualMachines/restart/action|Reinicia as máquinas virtuais.|
|/virtualMachines/stop/action|Paradas Olá máquina virtual.|
|/virtualMachines/shutdown/action|Olá desligar a máquina virtual.|
|/virtualMachines/attachDisk/action|Anexa uma máquina virtual de tooa de disco de dados.|
|/virtualMachines/detachDisk/action|Desanexa um disco de dados da máquina virtual.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/action|Baixa o arquivo RDP de saudação para a máquina virtual.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/read|Obtém o grupo de segurança de rede Olá associado Olá interface de rede.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/write|Adiciona um grupo de segurança de rede associado à interface de rede de saudação.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/delete|Exclui o grupo de segurança de rede Olá associado à interface de rede de saudação.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lê o status da operação de saudação para máquinas virtuais de saudação associados a grupos de segurança de rede.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/read|Obtém as definições de métricas de saudação.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/read|Obter configurações de diagnóstico de saudação.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/write|Adicionar ou modificar configurações de diagnóstico.|
|/virtualMachines/metrics/read|Obtém a métrica de saudação.|
|/virtualMachines/operationStatuses/read|Lê o status da operação Olá para máquinas virtuais de saudação.|
|/virtualMachines/extensions/read|Obtém a extensão da máquina virtual hello.|
|/virtualMachines/extensions/write|Coloca a extensão da máquina virtual hello.|
|/virtualMachines/extensions/operationStatuses/read|Lê o status da operação Olá para extensões de máquinas virtuais de saudação.|
|/virtualMachines/asyncOperations/read|Obtém as operações assíncronas possíveis de saudação|
|/virtualMachines/disks/read|Recupera a lista de discos de dados|
|/virtualMachines/associatedNetworkSecurityGroups/read|Obtém o grupo de segurança de rede Olá associado à máquina virtual de saudação.|
|/virtualMachines/associatedNetworkSecurityGroups/write|Adiciona um grupo de segurança de rede associado à máquina virtual de saudação.|
|/virtualMachines/associatedNetworkSecurityGroups/delete|Exclui o grupo de segurança de rede Olá associado à máquina virtual de saudação.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/read|Lê o status da operação de saudação para máquinas virtuais de saudação associados a grupos de segurança de rede.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Operação | Descrição |
|---|---|
|/register/action|Registrar tooClassic rede|
|/gatewaySupportedDevices/Read|Recupera a lista de saudação de dispositivos com suporte.|
|/reservedIps/read|Obtém Olá Ips reservados|
|/reservedIps/write|Adicionar um novo IP reservado|
|/reservedIps/delete|Excluir um IP reservado.|
|/reservedIps/link/action|Vincular um IP reservado|
|/reservedIps/join/action|Ingressar em um IP reservado|
|/reservedIps/operationStatuses/read|Lê o status da operação Olá para ips Olá reservado.|
|/virtualNetworks/read|Obtenha a rede virtual hello.|
|/virtualNetworks/write|Adicionar uma nova rede virtual.|
|/virtualNetworks/delete|Exclui a rede virtual hello.|
|/virtualNetworks/peer/action|Coloca uma rede virtual com outra rede virtual de mesmo nível.|
|/virtualNetworks/join/action|Ingressar na rede virtual hello.|
|/virtualNetworks/checkIPAddressAvailability/action|Olá verifica a disponibilidade de um endereço IP específico em uma rede virtual.|
|/virtualNetworks/capabilities/read|Mostra os recursos de saudação|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/read|Obtém o grupo de segurança de rede Olá associado Olá sub-rede.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/write|Adiciona um grupo de segurança de rede associado à sub-rede de saudação.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/delete|Exclui o grupo de segurança de rede Olá associado à sub-rede de saudação.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lê o status da operação Olá para grupos de segurança de rede Olá rede virtual sub-rede associados.|
|/virtualNetworks/operationStatuses/read|Lê o status da operação Olá para redes virtuais hello.|
|/virtualNetworks/gateways/read|Obtém os gateways de rede virtual hello.|
|/virtualNetworks/gateways/write|Adiciona um gateway de rede virtual.|
|/virtualNetworks/gateways/delete|Exclui o gateway de rede virtual hello.|
|/virtualNetworks/gateways/startDiagnostics/action|Inicia o diagnóstico de gateway de rede virtual hello.|
|/virtualNetworks/gateways/stopDiagnostics/action|Paradas Olá diagnóstico de gateway de rede virtual hello.|
|/virtualNetworks/gateways/downloadDiagnostics/action|Downloads de diagnóstico do gateway hello.|
|/virtualNetworks/gateways/listCircuitServiceKey/action|Recupera a chave de serviço do circuito hello.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/action|Baixa o script de configuração de dispositivo de saudação.|
|/virtualNetworks/gateways/listPackage/action|Lista o pacote de saudação do gateway de rede virtual.|
|/virtualNetworks/gateways/operationStatuses/read|Lê o status da operação Olá para gateways de redes virtuais hello.|
|/virtualNetworks/gateways/packages/read|Obtém o pacote de saudação do gateway de rede virtual.|
|/virtualNetworks/gateways/connections/read|Recupera a lista de saudação de conexões.|
|/virtualNetworks/gateways/connections/connect/action|Conecta-se uma conexão de gateway do site toosite.|
|/virtualNetworks/gateways/connections/disconnect/action|Desconecta uma conexão de gateway do site toosite.|
|/virtualNetworks/gateways/connections/test/action|Testa uma conexão de gateway do site toosite.|
|/virtualNetworks/gateways/clientRevokedCertificates/read|Saudação de leitura revogar certificados de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/write|Revoga um certificado de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/delete|Cancela a revogação de um certificado de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/read|Localize Olá certificados raiz do cliente.|
|/virtualNetworks/gateways/clientRootCertificates/write|Carrega um novo certificado raiz do cliente.|
|/virtualNetworks/gateways/clientRootCertificates/delete|Exclui o certificado de cliente de gateway de rede virtual hello.|
|/virtualNetworks/gateways/clientRootCertificates/download/action|Baixa o certificado por impressão digital.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/action|Lista o pacote de certificado de gateway de rede virtual hello.|
|/networkSecurityGroups/read|Obtém o grupo de segurança de rede de saudação.|
|/networkSecurityGroups/write|Adiciona um novo grupo de segurança de rede.|
|/networkSecurityGroups/delete|Exclui o grupo de segurança de rede de saudação.|
|/networkSecurityGroups/operationStatuses/read|Lê o status da operação Olá para o grupo de segurança de rede hello.|
|/networkSecurityGroups/securityRules/read|Obtém a regra de segurança de saudação.|
|/networkSecurityGroups/securityRules/write|Adiciona ou atualiza uma regra de segurança.|
|/networkSecurityGroups/securityRules/delete|Exclui a regra de segurança de saudação.|
|/networkSecurityGroups/securityRules/operationStatuses/read|Lê o status da operação Olá para regras de segurança de grupo de segurança de rede hello.|
|/quotas/read|Obter cota Olá Olá assinatura.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Operação | Descrição |
|---|---|
|/register/action|Registrar tooClassic armazenamento|
|/checkStorageAccountAvailability/action|Verifica se há disponibilidade de saudação de uma conta de armazenamento.|
|/capabilities/read|Mostra os recursos de saudação|
|/publicImages/read|Obtém a imagem de máquina virtual público hello.|
|/images/read|Imagem de saudação retorna.|
|/storageAccounts/read|Retorne conta de armazenamento Olá com hello dada conta.|
|/storageAccounts/write|Adiciona uma nova conta de armazenamento.|
|/storageAccounts/delete|Exclua a conta de armazenamento hello.|
|/storageAccounts/listKeys/action|Lista as chaves de acesso Olá Olá para contas de armazenamento.|
|/storageAccounts/regenerateKey/action|Regenera as chaves de acesso existentes Olá Olá conta de armazenamento.|
|/storageAccounts/operationStatuses/read|Lê o status da operação Olá para o recurso de saudação.|
|/storageAccounts/images/read|Retorna Olá imagem da conta de armazenamento.|
|/storageAccounts/images/delete|Excluir uma imagem da conta de armazenamento específica.|
|/storageAccounts/disks/read|Retorna Olá disco da conta de armazenamento.|
|/storageAccounts/disks/write|Adiciona um disco de conta de armazenamento.|
|/storageAccounts/disks/delete|Excluir um disco de conta de armazenamento específico.|
|/storageAccounts/disks/operationStatuses/read|Lê o status da operação Olá para o recurso de saudação.|
|/storageAccounts/osImages/read|Retorna Olá imagem de sistema operacional da conta de armazenamento.|
|/storageAccounts/osImages/delete|Excluir uma imagem do sistema operacional da conta de armazenamento específica.|
|/storageAccounts/services/read|Obter serviços disponíveis da saudação.|
|/storageAccounts/services/metricDefinitions/read|Obtém as definições de métricas de saudação.|
|/storageAccounts/services/metrics/read|Obtém a métrica de saudação.|
|/storageAccounts/services/diagnosticSettings/read|Obter configurações de diagnóstico de saudação.|
|/storageAccounts/services/diagnosticSettings/write|Adicionar ou modificar configurações de diagnóstico.|
|/disks/read|Retorna Olá disco da conta de armazenamento.|
|/osImages/read|Imagem do sistema operacional Olá retorna.|
|/quotas/read|Obter cota Olá Olá assinatura.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Operação | Descrição |
|---|---|
|/accounts/read|Ler as contas de API.|
|/accounts/write|Grava as contas de API.|
|/accounts/delete|Excluir contas de API|
|/accounts/listKeys/action|Listar chaves|
|/accounts/regenerateKey/action|Regenerar chave|
|/accounts/skus/read|Ler SKUs disponíveis para um recurso existente.|
|/accounts/usages/read|Obter a utilização de cota Olá para um recurso existente.|
|/Operations/read|Descrição da operação de saudação.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Operação | Descrição |
|---|---|
|/RateCard/read|Retorna oferece dados, metadados/medidor de recursos e as taxas de saudação assinatura determinada.|
|/UsageAggregates/read|Recupera o consumo do Microsoft Azure para uma assinatura. resultado Olá contém agregações de dados de uso, assinatura e recursos relacionados ao obter informações sobre um intervalo de tempo específico.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura com o provedor de recursos Microsoft.Compute|
|/restorePointCollections/read|Obter propriedades de saudação de uma coleção de ponto de restauração|
|/restorePointCollections/write|Criar uma nova coleção de pontos de restauração ou atualizar uma existente|
|/restorePointCollections/delete|Coleção de pontos de restauração exclusões hello e pontos de restauração independente|
|/restorePointCollections/restorePoints/read|Obter propriedades de saudação de um ponto de restauração|
|/restorePointCollections/restorePoints/write|Criar um novo ponto de restauração|
|/restorePointCollections/restorePoints/delete|Exclui o ponto de restauração Olá|
|/restorePointCollections/restorePoints/retrieveSasUris/action|Obter propriedades de saudação de um ponto de restauração com URIs de SAS do blob|
|/virtualMachineScaleSets/read|Obter propriedades de saudação de um conjunto de escala de máquinas virtuais|
|/virtualMachineScaleSets/write|Criar um novo conjunto de dimensionamento de máquinas virtuais ou atualizar um existente|
|/virtualMachineScaleSets/delete|Exclui o conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/start/action|Inicia Olá instâncias do conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/powerOff/action|Desliga a instâncias de saudação do conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/restart/action|Reinicia as instâncias de saudação do conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/deallocate/action|Desliga e recursos de computação de saudação de versões para instâncias de saudação do conjunto de escalas da máquina virtual Olá |
|/virtualMachineScaleSets/manualUpgrade/action|Atualiza manualmente o modelo de toolatest de instâncias do conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/scale/action|Reduzir ou escalar horizontalmente a contagem de instâncias de um conjunto de dimensionamento de máquinas virtuais existente|
|/virtualMachineScaleSets/instanceView/read|Obtém a exibição de instância de saudação do conjunto de escalas da máquina virtual Olá|
|/virtualMachineScaleSets/skus/read|Listas Olá SKUs válidos para um conjunto de escala de máquina virtual existente|
|/virtualMachineScaleSets/virtualMachines/read|Recupera as propriedades de saudação de uma máquina Virtual em um conjunto de escala de VM|
|/virtualMachineScaleSets/virtualMachines/delete|Excluir uma máquina virtual específica em um conjunto de dimensionamento de VM.|
|/virtualMachineScaleSets/virtualMachines/start/action|Iniciar uma instância de máquina virtual em um conjunto de dimensionamento de VM.|
|/virtualMachineScaleSets/virtualMachines/powerOff/action|Desligar uma instância de máquina virtual em um conjunto de dimensionamento de VM.|
|/virtualMachineScaleSets/virtualMachines/restart/action|Reiniciar uma instância de máquina virtual em um conjunto de dimensionamento de VM.|
|/virtualMachineScaleSets/virtualMachines/deallocate/action|Desliga e recursos de computação de saudação de versões para uma máquina Virtual em um conjunto de escala de VM.|
|/virtualMachineScaleSets/virtualMachines/instanceView/read|Recupera o modo de exibição de instância de saudação de uma máquina Virtual em um conjunto de escala de VM.|
|/images/read|Obter propriedades de saudação do hello imagem|
|/images/write|Criar uma nova imagem ou atualizar uma existente|
|/images/delete|Exclui a imagem de saudação|
|/operations/read|Listar as operações disponíveis no provedor de recursos Microsoft.Compute|
|/disks/read|Obter propriedades de saudação de um disco|
|/disks/write|Criar um novo disco ou atualizar um existente|
|/disks/delete|Exclusões Olá disco|
|/disks/beginGetAccess/action|Obter Olá URI SAS do disco de saudação para acesso de blob|
|/disks/endGetAccess/action|Revogar Olá URI SAS de saudação em disco|
|/snapshots/read|Obter propriedades de saudação de um instantâneo|
|/snapshots/write|Criar um novo instantâneo ou atualizar um existente|
|/snapshots/delete|Excluir um instantâneo|
|/availabilitySets/read|Obter propriedades de saudação de um conjunto de disponibilidade|
|/availabilitySets/write|Criar um novo conjunto de disponibilidade ou atualizar um existente|
|/availabilitySets/delete|Exclui o conjunto de disponibilidade Olá|
|/availabilitySets/vmSizes/read|Lista os tamanhos disponíveis para criar ou atualizar uma máquina virtual no conjunto de disponibilidade Olá|
|/virtualMachines/read|Obter propriedades de saudação de uma máquina virtual|
|/virtualMachines/write|Criar uma nova máquina virtual ou atualizar uma máquina virtual existente|
|/virtualMachines/delete|Exclui a máquina virtual de saudação|
|/virtualMachines/start/action|Olá inicia a máquina virtual|
|/virtualMachines/powerOff/action|Desliga Olá VM. Observe que a máquina virtual Olá continuará toobe cobrado.|
|/virtualMachines/redeploy/action|Reimplantar a máquina virtual|
|/virtualMachines/restart/action|Reinicia a máquina virtual de saudação|
|/virtualMachines/deallocate/action|Desliga a máquina virtual de saudação e versões Olá os recursos de computação|
|/virtualMachines/generalize/action|Define Olá tooGeneralized de estado de máquina virtual e prepara a máquina virtual de saudação para captura|
|/virtualMachines/capture/action|Captura de máquina virtual de saudação copiando discos rígidos virtuais e gera um modelo que pode ser usado toocreate máquinas de virtuais semelhantes|
|/virtualMachines/convertToManagedDisks/action|Converte os discos de blob com base em Olá de discos de toomanaged Olá máquina virtual|
|/virtualMachines/vmSizes/read|Lista os tamanhos disponíveis Olá VM pode ser atualizado para|
|/virtualMachines/instanceView/read|Obtém Olá status de execução detalhado da máquina virtual de saudação e seus recursos|
|/virtualMachines/extensions/read|Obter propriedades de saudação de uma extensão de máquina virtual|
|/virtualMachines/extensions/write|Criar uma nova extensão da máquina virtual ou atualizar uma existente|
|/virtualMachines/extensions/delete|Exclui a extensão da máquina virtual Olá|
|/locations/vmSizes/read|Listar os tamanhos de máquina virtual disponível em um local|
|/locations/usages/read|Obtém os limites de serviço e quantidades de uso atuais para recursos de computação da assinatura Olá em um local|
|/locations/operations/read|Obtém o status de saudação de uma operação assíncrona|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de registro de contêiner hello e permite a criação de saudação de registros do contêiner.|
|/checknameavailability/read|Verificar se esse nome de registro é válido e não está em uso.|
|/registries/read|Olá retorna a lista de registros de contêiner ou obtém Olá propriedades de registro de contêiner especificado hello.|
|/registries/write|Cria um registro de contêiner com hello parâmetros especificados ou atualizar propriedades de saudação ou marcações para registro de contêiner especificado hello.|
|/registries/delete|Excluir um registro de contêiner existente.|
|/registries/listCredentials/action|Lista as credenciais de logon de saudação para registro de contêiner especificado hello.|
|/registries/regenerateCredential/action|Regenera as credenciais de logon de saudação para registro de contêiner especificado hello.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Operação | Descrição |
|---|---|
|/containerServices/subscriptions/read|Get hello serviços de contêiner especificados com base na assinatura|
|/containerServices/resourceGroups/read|Get hello serviços de contêiner especificados com base no grupo de recursos|
|/containerServices/resourceGroups/ContainerServiceName/read|Obtém Olá especificado serviço de contêiner|
|/containerServices/resourceGroups/ContainerServiceName/write|Coloca ou Olá atualizações especificado serviço de contêiner|
|/containerServices/resourceGroups/ContainerServiceName/delete|Olá exclusões especificado serviço de contêiner|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Operação | Descrição |
|---|---|
|/updateCommunicationPreference/action|Atualizar as preferências de comunicação|
|/listCommunicationPreference/action|Listar preferência de comunicação|
|/applications/read|Operação de Leitura|
|/applications/write|Operação de Gravação|
|/applications/write|Operação de Gravação|
|/applications/delete|Operação de Exclusão|
|/applications/listSecrets/action|Listar segredos|
|/applications/listSingleSignOnToken/action|Ler tokens de logon único|
|/operations/read|operações de leitura|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Operação | Descrição |
|---|---|
|/hubs/read|Ler Hub de informações do Customer Insights|
|/hubs/write|Criar ou atualizar um Hub de informações do Customer Insights|
|/hubs/delete|Excluir Hub de informações do Customer Insights|
|/hubs/providers/Microsoft.Insights/metricDefinitions/read|Obtém métricas disponíveis Olá para recursos|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/read|Obtém a configuração de diagnóstico de saudação para o recurso de saudação|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/write|Cria ou atualiza a configuração de diagnóstico de saudação para o recurso de saudação|
|/hubs/providers/Microsoft.Insights/logDefinitions/read|Obtém os logs disponíveis Olá para o recurso|
|/hubs/authorizationPolicies/read|Ler política de assinatura de acesso compartilhado do Azure Customer Insights|
|/hubs/authorizationPolicies/write|Criar ou atualizar política de assinatura de acesso compartilhado do Azure Customer Insights|
|/hubs/authorizationPolicies/delete|Excluir política de assinatura de acesso compartilhado do Azure Customer Insights|
|/hubs/authorizationPolicies/regeneratePrimaryKey/action|Regenerar a chave primária da política de Assinatura de Acesso Compartilhado do Azure Customer Insights|
|/hubs/authorizationPolicies/regenerateSecondaryKey/action|Regenerar a chave secundária da política de Assinatura de Acesso Compartilhado do Azure Customer Insights|
|/hubs/profiles/read|Ler perfil do Azure Customer Insights|
|/hubs/profiles/write|Gravar qualquer perfil do Azure Customer Insights|
|/hubs/kpi/read|Ler indicador principal de desempenho do Azure Customer Insights|
|/hubs/kpi/write|Criar ou atualizar indicador principal de desempenho do Azure Customer Insights|
|/hubs/kpi/delete|Excluir indicador principal de desempenho do Azure Customer Insights|
|/hubs/views/read|Ler modo de exibição de aplicativo do Azure Customer Insights|
|/hubs/views/write|Criar ou atualizar modo de exibição de aplicativo do Azure Customer Insights|
|/hubs/views/delete|Excluir modo de exibição de aplicativo do Azure Customer Insights|
|/hubs/interactions/read|Ler interação do Azure Customer Insights|
|/hubs/interactions/write|Criar ou atualizar interação do Azure Customer Insights|
|/hubs/roleAssignments/read|Ler atribuição RBAC do Azure Customer Insights|
|/hubs/roleAssignments/write|Criar ou atualizar atribuição RBAC do Azure Customer Insights|
|/hubs/roleAssignments/delete|Excluir atribuição RBAC do Azure Customer Insights|
|/hubs/connectors/read|Ler conector do Azure Customer Insights|
|/hubs/connectors/write|Criar ou atualizar conector do Azure Customer Insights|
|/hubs/connectors/delete|Excluir conector do Azure Customer Insights|
|/hubs/connectors/mappings/read|Ler mapeamento do conector do Azure Customer Insights|
|/hubs/connectors/mappings/write|Criar ou atualizar mapeamento de conector do Azure Customer Insights|
|/hubs/connectors/mappings/delete|Excluir mapeamento do conector do Azure Customer Insights|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Operação | Descrição |
|---|---|
|/checkNameAvailability/action|Verificar a disponibilidade do nome do catálogo para o locatário.|
|/catalogs/read|Obter propriedades dos catálogos na assinatura ou no grupo de recursos.|
|/catalogs/write|Cria catálogo ou atualizações de marcas de saudação e as propriedades de catálogo hello.|
|/catalogs/delete|Exclui o catálogo de saudação.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Operação | Descrição |
|---|---|
|/datafactories/read|Ler Data Factory.|
|/datafactories/write|Criar ou atualizar data factory|
|/datafactories/delete|Excluir o data factory.|
|/datafactories/datapipelines/read|Ler pipeline.|
|/datafactories/datapipelines/delete|Excluir o pipeline.|
|/datafactories/datapipelines/pause/action|Pausar pipeline.|
|/datafactories/datapipelines/resume/action|Retomar pipeline.|
|/datafactories/datapipelines/update/action|Atualizar pipeline.|
|/datafactories/datapipelines/write|Criar ou atualizar pipeline|
|/datafactories/linkedServices/read|Ler serviço vinculado.|
|/datafactories/linkedServices/delete|Excluir o serviço vinculado.|
|/datafactories/linkedServices/write|Criar ou atualizar serviço vinculado|
|/datafactories/tables/read|Ler tabela.|
|/datafactories/tables/delete|Excluir a tabela.|
|/datafactories/tables/write|Criar ou atualizar tabela|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Operação | Descrição |
|---|---|
|/accounts/read|Obter informações sobre Olá DataLakeAnalytics conta.|
|/accounts/write|Criar ou atualizar a conta de DataLakeAnalytics hello.|
|/accounts/delete|Exclua a conta de DataLakeAnalytics hello.|
|/accounts/firewallRules/read|Obter informações sobre uma regra de firewall.|
|/accounts/firewallRules/write|Criar ou atualizar uma regra de firewall.|
|/accounts/firewallRules/delete|Excluir uma regra de firewall.|
|/accounts/storageAccounts/read|Obter a conta de armazenamento vinculada para Olá DataLakeAnalytics conta.|
|/accounts/storageAccounts/write|Vincule uma conta de armazenamento toohello DataLakeAnalytics conta.|
|/accounts/storageAccounts/delete|Desvincule uma conta de armazenamento de saudação DataLakeAnalytics conta.|
|/accounts/storageAccounts/Containers/read|Obter contêineres em Olá conta de armazenamento|
|/accounts/storageAccounts/Containers/listSasTokens/action|Lista de Tokens de SAS Olá contêiner de armazenamento|
|/accounts/dataLakeStoreAccounts/read|Obter conta DataLakeStore vinculada Olá DataLakeAnalytics conta.|
|/accounts/dataLakeStoreAccounts/write|Vincule uma conta de DataLakeStore toohello DataLakeAnalytics conta.|
|/accounts/dataLakeStoreAccounts/delete|Desvincule uma conta de DataLakeStore de saudação DataLakeAnalytics conta.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Operação | Descrição |
|---|---|
|/accounts/read|Obter informações sobre uma conta DataLakeStore existente.|
|/accounts/write|Criar uma nova conta de DataLakeStore ou atualizar uma conta DataLakeStore existente.|
|/accounts/delete|Excluir uma conta existente do DataLakeStore.|
|/accounts/firewallRules/read|Obter informações sobre uma regra de firewall.|
|/accounts/firewallRules/write|Criar ou atualizar uma regra de firewall.|
|/accounts/firewallRules/delete|Excluir uma regra de firewall.|
|/accounts/trustedIdProviders/read|Obter informações sobre um provedor de identidade confiável.|
|/accounts/trustedIdProviders/write|Criar ou atualizar um provedor de identidade confiável.|
|/accounts/trustedIdProviders/delete|Excluir um provedor de identidade confiável.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Operação | Descrição |
|---|---|
|/register/action|Registrar assinatura Olá Olá hub IOT recurso provedor e permite Olá para a criação de recursos de Hub IOT|
|/checkNameAvailability/Action|Verificar se o nome do IotHub está disponível|
|/usages/Read|Obter detalhes de uso de assinatura para esse provedor.|
|/operations/Read|Obter todas as operações de ResourceProvider|
|/iotHubs/Read|Obtém os recursos do hub IOT Olá|
|/iotHubs/Write|Criar ou atualizar recursos IotHub|
|/iotHubs/Delete|Excluir recurso IotHub|
|/iotHubs/listkeys/Action|Obter todas as chaves IotHub|
|/iotHubs/exportDevices/Action|Exportar dispositivos|
|/iotHubs/importDevices/Action|Importar dispositivos|
|/IotHubs/metricDefinitions/read|Obtém métricas disponíveis Olá Olá serviço hub IOT|
|/iotHubs/iotHubKeys/listkeys/Action|Obter IotHub Key para nome Olá|
|/iotHubs/iotHubStats/Read|Obter estatísticas de IotHub|
|/iotHubs/quotaMetrics/Read|Obter métrica de cota|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Criar grupo de consumidores EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Obter grupo de consumidores EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Delete|Excluir grupo de consumidores EventHub|
|/iotHubs/routing/routes/$testall/Action|Testar uma mensagem com todas as rotas existentes|
|/iotHubs/routing/routes/$testnew/Action|Testar uma mensagem em uma rota de teste fornecida|
|/IotHubs/diagnosticSettings/read|Obtém a configuração de diagnóstico de saudação para o recurso de saudação|
|/IotHubs/diagnosticSettings/write|Cria ou atualiza a configuração de diagnóstico de saudação para o recurso de saudação|
|/iotHubs/skus/Read|Obter SKUs IotHub válidos|
|/iotHubs/jobs/Read|Obter detalhes de trabalhos enviados em determinado IotHub|
|/iotHubs/routingEndpointsHealth/Read|Obtém a integridade de saudação de todos os pontos de extremidade de roteamentos para um hub IOT|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Operação | Descrição |
|---|---|
|/Subscription/register/action|Registra a assinatura de saudação|
|/labs/delete|Excluir laboratórios.|
|/labs/read|Ler laboratórios.|
|/labs/write|Adicionar ou modificar os laboratórios.|
|/labs/ListVhds/action|Listar imagens de disco disponíveis para a criação de imagens personalizadas.|
|/labs/GenerateUploadUri/action|Gere um URI para carregar as imagens de disco personalizada tooa laboratório.|
|/labs/CreateEnvironment/action|Criar máquinas virtuais em um laboratório.|
|/labs/ClaimAnyVm/action|Declaração de uma máquina virtual claimable aleatória no laboratório de saudação.|
|/labs/ExportResourceUsage/action|Exportações Olá o uso de recursos do laboratório em uma conta de armazenamento|
|/labs/users/delete|Excluir perfis de usuário.|
|/labs/users/read|Ler perfis de usuário.|
|/labs/users/write|Adicionar ou modificar perfis de usuário.|
|/labs/users/secrets/delete|Excluir segredos.|
|/labs/users/secrets/read|Ler segredos.|
|/labs/users/secrets/write|Adicionar ou modificar segredos.|
|/labs/users/environments/delete|Excluir ambientes.|
|/labs/users/environments/read|Ler ambientes.|
|/labs/users/environments/write|Adicionar ou modificar ambientes.|
|/labs/users/disks/delete|Excluir discos.|
|/labs/users/disks/read|Ler discos.|
|/labs/users/disks/write|Adicionar ou modificar discos.|
|/labs/users/disks/Attach/action|Anexar e criar concessão de saudação da máquina virtual do hello disco toohello.|
|/labs/users/disks/Detach/action|Desanexar e concessão de saudação quebra do disco Olá anexado toohello VM.|
|/labs/customImages/delete|Excluir imagens personalizadas.|
|/labs/customImages/read|Ler imagens personalizadas.|
|/labs/customImages/write|Adicionar ou modificar imagens personalizadas.|
|/labs/serviceRunners/delete|Excluir executores de serviço.|
|/labs/serviceRunners/read|Ler os executores de serviço.|
|/labs/serviceRunners/write|Adicionar ou modificar os executores de serviço.|
|/labs/artifactSources/delete|Excluir fontes de artefato.|
|/labs/artifactSources/read|Ler fontes de artefato.|
|/labs/artifactSources/write|Adicionar ou modificar fontes de artefato.|
|/labs/artifactSources/artifacts/read|Ler artefatos.|
|/labs/artifactSources/artifacts/GenerateArmTemplate/action|Gera um modelo do ARM para Olá fornecido artefato, carrega a conta de armazenamento de tooa Olá necessários arquivos e valida o artefato Olá gerado.|
|/labs/artifactSources/armTemplates/read|Ler modelos do Azure Resource Manager.|
|/labs/costs/read|Ler custos.|
|/labs/costs/write|Adicionar ou modificar custos.|
|/labs/virtualNetworks/delete|Excluir redes virtuais.|
|/labs/virtualNetworks/read|Ler redes virtuais.|
|/labs/virtualNetworks/write|Adicionar ou modificar redes virtuais.|
|/labs/formulas/delete|Excluir fórmulas.|
|/labs/formulas/read|Ler fórmulas.|
|/labs/formulas/write|Adicionar ou modificar fórmulas.|
|/labs/schedules/delete|Excluir agendas.|
|/labs/schedules/read|Ler agendas.|
|/labs/schedules/write|Adicionar ou modificar agendamentos.|
|/labs/schedules/Execute/action|Executar uma agenda.|
|/labs/schedules/ListApplicable/action|Listar todas as agendas aplicáveis|
|/labs/galleryImages/read|Ler imagens da galeria.|
|/labs/policySets/EvaluatePolicies/action|Avaliar a política de laboratório.|
|/labs/policySets/policies/delete|Excluir políticas.|
|/labs/policySets/policies/read|Ler políticas.|
|/labs/policySets/policies/write|Adicionar ou modificar políticas.|
|/labs/virtualMachines/delete|Excluir as máquinas virtuais.|
|/labs/virtualMachines/read|Ler máquinas virtuais.|
|/labs/virtualMachines/write|Adicionar ou modificar máquinas virtuais.|
|/labs/virtualMachines/Start/action|Iniciar uma máquina virtual.|
|/labs/virtualMachines/Stop/action|Parar uma máquina virtual|
|/labs/virtualMachines/ApplyArtifacts/action|Aplica a máquina de toovirtual de artefatos.|
|/labs/virtualMachines/AddDataDisk/action|Anexe uma máquina de toovirtual de disco de dados novo ou existente.|
|/labs/virtualMachines/DetachDataDisk/action|Desanexe o disco especificado de saudação da máquina virtual de saudação.|
|/labs/virtualMachines/Claim/action|Assumir o controle de uma máquina virtual existente|
|/labs/virtualMachines/ListApplicableSchedules/action|Listar todas as agendas aplicáveis|
|/labs/virtualMachines/schedules/delete|Excluir agendas.|
|/labs/virtualMachines/schedules/read|Ler agendas.|
|/labs/virtualMachines/schedules/write|Adicionar ou modificar agendamentos.|
|/labs/virtualMachines/schedules/Execute/action|Executar uma agenda.|
|/labs/notificationChannels/delete|Excluir notificationchannels.|
|/labs/notificationChannels/read|Ler notificationchannels.|
|/labs/notificationChannels/write|Adicionar ou modificar notificationchannels.|
|/labs/notificationChannels/Notify/action|Envie o canal de notificação de tooprovided.|
|/schedules/delete|Excluir agendas.|
|/schedules/read|Ler agendas.|
|/schedules/write|Adicionar ou modificar agendamentos.|
|/schedules/Execute/action|Executar uma agenda.|
|/schedules/Retarget/action|Atualizar ID de recurso de destino de uma agenda.|
|/locations/operations/read|Operações de leitura.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Operação | Descrição |
|---|---|
|/databaseAccountNames/read|Verificar a disponibilidade do nome.|
|/databaseAccounts/read|Ler uma conta de banco de dados.|
|/databaseAccounts/write|Atualizar uma conta de banco de dados.|
|/databaseAccounts/listKeys/action|Listar chaves de uma conta de banco de dados|
|/databaseAccounts/regenerateKey/action|Girar chaves de uma conta de banco de dados|
|/databaseAccounts/listConnectionStrings/action|Obter cadeias de caracteres de conexão Olá para uma conta de banco de dados|
|/databaseAccounts/changeResourceGroup/action|Alterar o grupo de recursos de uma conta de banco de dados|
|/databaseAccounts/failoverPriorityChange/action|Alterar as prioridades de failover das regiões de uma conta de banco de dados. Isso é usado tooperform operação de failover manual|
|/databaseAccounts/delete|Exclui Olá contas de banco de dados.|
|/databaseAccounts/metricDefinitions/read|Lê definições de métricas de conta de banco de dados de saudação.|
|/databaseAccounts/metrics/read|Lê as métricas Olá da conta do banco de dados.|
|/databaseAccounts/usages/read|Lê os usos de conta do banco de dados de saudação.|
|/databaseAccounts/databases/collections/metricDefinitions/read|Lê a coleção de saudação definições de métrica.|
|/databaseAccounts/databases/collections/metrics/read|Lê as métricas de coleção de saudação.|
|/databaseAccounts/databases/collections/usages/read|Lê os usos de coleção de saudação.|
|/databaseAccounts/databases/metricDefinitions/read|Lê definições de métricas de banco de dados de saudação|
|/databaseAccounts/databases/metrics/read|Lê as métricas de banco de dados de saudação.|
|/databaseAccounts/databases/usages/read|Lê os usos do banco de dados de saudação.|
|/databaseAccounts/readonlykeys/read|Lê a conta de banco de dados de saudação chaves somente leitura.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Operação | Descrição |
|---|---|
|/generateSsoRequest/Action|Gerar uma solicitação para entrar no centro de controle de domínio.|
|/validateDomainRegistrationInformation/Action|Validar o objeto de compra de domínio sem enviá-lo|
|/checkDomainAvailability/Action|Verificar se um domínio está disponível para compra|
|/listDomainRecommendations/Action|Recuperar Olá lista as recomendações de domínio com base em palavras-chave|
|/register/action|Registrar o provedor de recursos Microsoft Domains Olá para assinatura de saudação|
|/domains/Read|Obter lista de saudação de domínios|
|/domains/Write|Adicionar um novo domínio ou atualizar um existente|
|/domains/Delete|Excluir um modo de exibição existente.|
|/domains/operationresults/Read|Obter uma operação de domínio|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Operação | Descrição |
|---|---|
|/lcsprojects/read|Exibir projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem a usuário tooa|
|/lcsprojects/write|Criar e atualizar os projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem a usuário toohello. Apenas propriedades de nome e uma descrição da saudação podem ser atualizadas. assinatura de saudação e no local associados ao projeto de saudação não podem ser atualizadas após a criação|
|/lcsprojects/delete|Excluir projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem a usuário toohello|
|/lcsprojects/clouddeployments/read|Exibir as implantações de avaliação do Microsoft Dynamics AX 2012 R3 em um projeto de serviços de ciclo de vida do Microsoft Dynamics que pertence a usuário tooa|
|/lcsprojects/clouddeployments/write|Crie implantação de avaliação do Microsoft Dynamics AX 2012 R3 em um projeto de serviços de ciclo de vida do Microsoft Dynamics que pertence a usuário tooa. As implantações podem ser gerenciadas no portal de gerenciamento do Azure|
|/lcsprojects/connectors/read|Leia os conectores que pertencem o projeto de serviços de ciclo de vida do Microsoft Dynamics tooa|
|/lcsprojects/connectors/write|Criar e atualizar os conectores que pertencem o projeto de serviços de ciclo de vida do Microsoft Dynamics tooa|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Operação | Descrição |
|---|---|
|/checkNameAvailability/action|Verificar a disponibilidade do namespace em determinada assinatura.|
|/register/action|Registra a assinatura Olá para o provedor de recursos do EventHub hello e permite a criação de saudação dos recursos do Eventbus|
|/namespaces/write|Criar um recurso de namespace e atualizar suas propriedades. Marcações e status do Namespace de saudação são propriedades de saudação que podem ser atualizadas.|
|/namespaces/read|Obter lista de saudação da descrição do recurso de Namespace|
|/namespaces/Delete|Excluir o recurso de namespace|
|/namespaces/metricDefinitions/read|Obter lista de métrica de descrições de recurso de métrica do namespace|
|/namespaces/authorizationRules/read|Obter lista de saudação da descrição de regras de autorização de Namespaces.|
|/namespaces/authorizationRules/write|Criar regras de autorização no nível do namespace e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/authorizationRules/delete|Excluir regra de autorização de namespace. saudação de regra de autorização de Namespace padrão não pode ser excluída. |
|/namespaces/authorizationRules/listkeys/action|Obter cadeia de caracteres de Conexão de saudação toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Regenerar Olá primário ou secundário chave toohello recursos|
|/namespaces/eventhubs/write|Criar ou atualizar propriedades EventHub.|
|/namespaces/eventhubs/read|Obter lista de descrições de recursos de EventHub|
|/namespaces/eventhubs/Delete|Toodelete operação recurso do EventHub|
|/namespaces/eventHubs/consumergroups/write|Criar ou atualizar propriedades ConsumerGroup.|
|/namespaces/eventHubs/consumergroups/read|Obter lista de descrições de recursos ConsumerGroup|
|/namespaces/eventHubs/consumergroups/Delete|Toodelete operação recurso o ConsumerGroup|
|/namespaces/eventhubs/authorizationRules/read| Obter lista de saudação EventHub de regras de autorização|
|/namespaces/eventhubs/authorizationRules/write|Criar regras de autorização EventHub e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/eventhubs/authorizationRules/delete|Operação toodelete EventHub as regras de autorização|
|/namespaces/eventhubs/authorizationRules/listkeys/action|Obter Olá tooEventHub de cadeia de caracteres de Conexão|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/action|Regenerar Olá primário ou secundário chave toohello recursos|
|/namespaces/diagnosticSettings/read|Obter lista de descrições de recurso de configurações de diagnóstico do namespace|
|/namespaces/diagnosticSettings/write|Obter lista de descrições de recurso de configurações de diagnóstico do namespace|
|/namespaces/logDefinitions/read|Obter lista de descrições do recurso de log do namespace|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Operação | Descrição |
|---|---|
|/providers/features/read|Obtém o recurso de saudação de uma assinatura em um determinado provedor de recursos.|
|/providers/features/register/action|Registra o recurso Olá para uma assinatura em um determinado provedor de recursos.|
|/features/read|Obtém os recursos de saudação de uma assinatura.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Operação | Descrição |
|---|---|
|/clusters/write|Criar ou atualizar o Cluster HDInsight|
|/clusters/read|Obter detalhes sobre o Cluster HDInsight|
|/clusters/delete|Excluir um cluster HDInsight|
|/clusters/changerdpsetting/action|Alterar configuração de RDP para Cluster HDInsight|
|/clusters/configurations/action|Atualizar a configuração do Cluster HDInsight|
|/clusters/configurations/read|Obter configurações de Cluster HDInsight|
|/clusters/roles/resize/action|Redimensionar um cluster HDInsight|
|/locations/capabilities/read|Obter recursos de assinatura|
|/locations/checkNameAvailability/read|Verificar disponibilidade do nome|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de importação/exportação hello e permite a criação de saudação de trabalhos de importação/exportação.|
|/jobs/write|Cria um trabalho com hello parâmetros especificados ou atualizar propriedades de saudação ou marcações para o trabalho especificado hello.|
|/jobs/read|Obtém as propriedades de saudação do trabalho especificado hello ou retorna a lista de saudação de trabalhos.|
|/jobs/listBitLockerKeys/action|Obtém as chaves do BitLocker Olá para o trabalho especificado Olá.|
|/jobs/delete|Excluir um trabalho existente.|
|/locations/read|Obtém propriedades Olá Olá local ou retorna Olá lista especificada de locais.|

## <a name="microsoftinsights"></a>Microsoft.insights

| Operação | Descrição |
|---|---|
|/Register/Action|Registrar o provedor de informações do microsoft hello|
|/AlertRules/Write|Configuração de regra de alerta de tooan de gravação|
|/AlertRules/Delete|Excluir uma configuração de regra de alerta|
|/AlertRules/Read|Ler uma configuração de regra de alerta|
|/AlertRules/Activated/Action|Regra de alerta ativada|
|/AlertRules/Resolved/Action|Regra de alerta resolvida|
|/AlertRules/Throttled/Action|A regra de alerta está limitada|
|/AlertRules/Incidents/Read|Ler uma configuração incidente da regra de alerta|
|/MetricDefinitions/Read|Ler definições de métrica|
|/eventtypes/values/Read|Ler valores do tipo de evento de gerenciamento|
|/eventtypes/digestevents/Read|Ler resumo do tipo de evento de gerenciamento|
|/Metrics/Read|Ler métrica|
|/LogProfiles/Write|Gravar a configuração de perfil de registro tooa|
|/LogProfiles/Delete|Excluir configuração de perfis de log|
|/LogProfiles/Read|Ler perfis de log|
|/AutoscaleSettings/Write|Gravar a configuração de AutoEscala tooan|
|/AutoscaleSettings/Delete|Excluir uma configuração de dimensionamento automático|
|/AutoscaleSettings/Read|Ler uma configuração de dimensionamento automático|
|/AutoscaleSettings/Scaleup/Action|Dimensionar operação de escalada vertical automaticamente|
|/AutoscaleSettings/Scaledown/Action|Dimensionar operação de redução vertical automaticamente|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Ler definições de métrica|
|/ActivityLogAlerts/Activated/Action|Disparado hello atividade de Log de alerta|
|/DiagnosticSettings/Write|Gravação toodiagnostic definições de configuração|
|/DiagnosticSettings/Delete|Excluir configuração de diagnóstico|
|/DiagnosticSettings/Read|Ler uma configuração de diagnóstico|
|/LogDefinitions/Read|Ler definições de log|
|/ExtendedDiagnosticSettings/Write|Configuração de configurações de diagnóstico de tooextended de gravação|
|/ExtendedDiagnosticSettings/Delete|Excluir configuração de diagnóstico estendido|
|/ExtendedDiagnosticSettings/Read|Ler uma configuração de diagnóstico estendido|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Operação | Descrição |
|---|---|
|/register/action|Registrar uma assinatura|
|/checkNameAvailability/read|Verificar se um nome de chave do cofre é válido e não está em uso|
|/vaults/read|Exibir propriedades de saudação de um cofre de chaves|
|/vaults/write|Criar um novo Olá chave de cofre ou atualização propriedades de um cofre de chave existente|
|/vaults/delete|Excluir um cofre de chaves|
|/vaults/deploy/action|Habilita toosecrets em um cofre de chaves de acesso ao implantar os recursos do Azure|
|/vaults/secrets/read|Exibir propriedades de saudação de um segredo, mas não seu valor|
|/vaults/secrets/write|Crie um novo valor de saudação de segredo ou atualização de um segredo existente|
|/vaults/accessPolicies/write|Atualizar uma política de acesso de mesclagem ou substituindo ou adicionar um novo cofre de tooa de política de acesso.|
|/deletedVaults/read|Exibir propriedades de saudação do software excluído cofres de chaves|
|/locations/operationResults/read|Resultado da verificação de saudação de uma operação de longa execução|
|/locations/deletedVaults/read|Exibir propriedades de saudação de um cofre de chaves excluído flexível|
|/locations/deletedVaults/purge/action|Limpar um cofre de chaves com exclusão reversível|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Operação | Descrição |
|---|---|
|/workflows/read|Lê o fluxo de trabalho de saudação.|
|/workflows/write|Cria ou atualiza o fluxo de trabalho de saudação.|
|/workflows/delete|Exclui o fluxo de trabalho de saudação.|
|/workflows/run/action|Inicia uma execução de fluxo de trabalho de saudação.|
|/workflows/disable/action|Desabilita o fluxo de trabalho de saudação.|
|/workflows/enable/action|Permite que o fluxo de trabalho de saudação.|
|/workflows/validate/action|Valida o fluxo de trabalho de saudação.|
|/workflows/move/action|Move o fluxo de trabalho de sua existente id de assinatura, o grupo de recursos e/ou a id de assinatura diferente do nome tooa, grupo de recursos, e/ou nome.|
|/workflows/listSwagger/action|Obtém o fluxo de trabalho Olá definições de swagger.|
|/workflows/regenerateAccessKey/action|Regenera os segredos de chave de acesso de saudação.|
|/workflows/listCallbackUrl/action|Obtém a URL de retorno de chamada Olá para fluxo de trabalho.|
|/workflows/versions/read|Lê a versão de fluxo de trabalho de saudação.|
|/workflows/versions/triggers/listCallbackUrl/action|Obtém o URL de retorno de chamada de saudação do gatilho.|
|/workflows/runs/read|Lê o fluxo de trabalho Olá executar.|
|/workflows/runs/cancel/action|Cancela a execução de saudação de um fluxo de trabalho.|
|/workflows/runs/actions/read|Lê o fluxo de trabalho Olá executar a ação.|
|/workflows/runs/operations/read|Lê o status da operação de execução de fluxo de trabalho do hello.|
|/workflows/triggers/read|Lê o gatilho de saudação.|
|/workflows/triggers/run/action|Executa o gatilho de saudação.|
|/workflows/triggers/listCallbackUrl/action|Obtém o URL de retorno de chamada de saudação do gatilho.|
|/workflows/triggers/histories/read|Lê os históricos de gatilho hello.|
|/workflows/triggers/histories/resubmit/action|Reenvia gatilho do fluxo de trabalho de saudação.|
|/workflows/accessKeys/read|Lê a chave de acesso de saudação.|
|/workflows/accessKeys/write|Cria ou atualiza a chave de acesso de saudação.|
|/workflows/accessKeys/delete|Exclui a chave de acesso de saudação.|
|/workflows/accessKeys/list/action|Lista os segredos de chave de acesso de saudação.|
|/workflows/accessKeys/regenerate/action|Regenera os segredos de chave de acesso de saudação.|
|/locations/workflows/validate/action|Valida o fluxo de trabalho de saudação.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de serviço web de aprendizado de máquina hello e permite a criação de saudação de serviços web.|
|/webServices/action|Criar propriedades do serviço Web regionais para regiões com suporte|
|/commitmentPlans/read|Ler um plano de compromisso de Machine Learning|
|/commitmentPlans/write|Criar ou atualizar plano de compromisso de Machine Learning|
|/commitmentPlans/delete|Excluir plano de compromisso de Machine Learning|
|/commitmentPlans/join/action|Ingressar em um plano de compromisso de Machine Learning|
|/commitmentPlans/commitmentAssociations/read|Ler associações de plano de compromisso de Machine Learning|
|/commitmentPlans/commitmentAssociations/move/action|Mover associações de plano de compromisso de Machine Learning|
|/Workspaces/read|Ler um Espaço de Trabalho do Machine Learning|
|/Workspaces/write|Criar ou atualizar Espaço de Trabalho do Machine Learning|
|/Workspaces/delete|Criar um Espaço de Trabalho do Machine Learning|
|/Workspaces/listworkspacekeys/action|Listar chaves para um Espaço de Trabalho do Machine Learning|
|/Workspaces/resyncstoragekeys/action|Ressincronizar as chaves da conta de armazenamento configurada para um Espaço de Trabalho do Machine Learning|
|/webServices/read|Ler um serviço Web do Machine Learning|
|/webServices/write|Criar ou atualizar serviço Web do Machine Learning|
|/webServices/delete|Excluir um serviço Web do Machine Learning|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Operação | Descrição |
|---|---|
|/agreements/offers/plans/read|Retornar um contrato para um item específico do marketplace|
|/agreements/offers/plans/sign/action|Assinar um contrato para um item específico do marketplace|
|/agreements/offers/plans/cancel/action|Cancelar um contrato para um item específico do marketplace|

## <a name="microsoftmedia"></a>Microsoft.Media

| Operação | Descrição |
|---|---|
|/mediaservices/read||
|/mediaservices/write||
|/mediaservices/delete||
|/mediaservices/regenerateKey/action||
|/mediaservices/listKeys/action||
|/mediaservices/syncStorageKeys/action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura de saudação|
|/unregister/action|Cancela o registro de assinatura de saudação|
|/checkTrafficManagerNameAvailability/action|Olá verifica a disponibilidade de um nome DNS do Traffic Manager relativo.|
|/dnszones/read|Obtenha a zona do DNS hello, no formato JSON. Propriedades da zona Olá incluem marcas, etag, numberOfRecordSets e maxNumberOfRecordSets. Observe que esse comando não recupera conjuntos de registros Olá contidos Olá zona.|
|/dnszones/write|Criar ou atualizar uma zona DNS em um grupo de recursos.  Marcas de saudação tooupdate usado em um recurso de zona DNS. Observe que esse comando não pode ser usado toocreate ou atualizar conjuntos de registros na zona de saudação.|
|/dnszones/delete|Exclua a zona do DNS de hello, no formato JSON. Propriedades da zona Olá incluem marcas, etag, numberOfRecordSets e maxNumberOfRecordSets.|
|/dnszones/MX/read|Obter conjunto de registros de saudação do tipo 'MX', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/MX/write|Criar ou atualizar um conjunto de registros do tipo 'MX' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/MX/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'MX' de uma zona DNS.|
|/dnszones/NS/read|Obter o conjunto de registros DNS do tipo NS|
|/dnszones/NS/write|Criar ou atualizar o conjunto de registros DNS do tipo NS|
|/dnszones/NS/delete|Exclui o conjunto de registros de DNS de saudação do tipo NS|
|/dnszones/AAAA/read|Obter conjunto de registros de saudação do tipo 'AAAA', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/AAAA/write|Criar ou atualizar um conjunto de registros do tipo 'AAAA' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/AAAA/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'AAAA' de uma zona DNS.|
|/dnszones/CNAME/read|Obter conjunto de registros de saudação do tipo 'CNAME', no formato JSON. conjunto de registros de saudação contém Olá TTL, marcas e etag.|
|/dnszones/CNAME/write|Criar ou atualizar um conjunto de registros do tipo 'CNAME' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/CNAME/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'CNAME' de uma zona DNS.|
|/dnszones/SOA/read|Obter o conjunto de registros DNS do tipo SOA|
|/dnszones/SOA/write|Criar ou atualizar o conjunto de registros DNS do tipo SOA|
|/dnszones/SRV/read|Obter conjunto de registros de saudação do tipo 'SRV', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/SRV/write|Criar ou atualizar o conjunto de registros do tipo SRV|
|/dnszones/SRV/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'SRV' de uma zona DNS.|
|/dnszones/PTR/read|Obter conjunto de registros de saudação do tipo 'PTR', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/PTR/write|Criar ou atualizar um conjunto de registros do tipo 'PTR' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/PTR/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'PTR' de uma zona DNS.|
|/dnszones/A/read|Obter conjunto de registros de saudação do tipo 'A', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/A/write|Criar ou atualizar um conjunto de registros do tipo 'A' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/A/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'A' de uma zona DNS.|
|/dnszones/TXT/read|Obter conjunto de registros de saudação do tipo 'TXT', no formato JSON. conjunto de registros de saudação contém uma lista de registros, bem como Olá TTL, marcas e etag.|
|/dnszones/TXT/write|Criar ou atualizar um conjunto de registros do tipo 'TXT' em uma zona DNS. registros de saudação especificados substituirão os registros de atual de saudação no conjunto de registros de saudação.|
|/dnszones/TXT/delete|Remova o conjunto de registros de saudação de um determinado nome e tipo 'TXT' de uma zona DNS.|
|/dnszones/recordsets/read|Obter os conjuntos de registros DNS em todos os tipos|
|/networkInterfaces/read|Obter uma definição de adaptador de rede. |
|/networkInterfaces/write|Criar uma interface de rede ou atualizar uma interface de rede existente. |
|/networkInterfaces/join/action|Une uma interface de rede de tooa da máquina Virtual|
|/networkInterfaces/delete|Excluir um adaptador de rede|
|/networkInterfaces/effectiveRouteTable/action|Obter tabela de rota configurado na Interface de rede de Vm de saudação|
|/networkInterfaces/effectiveNetworkSecurityGroups/action|Obter grupos de segurança de rede na rede Interface de saudação configurado Vm|
|/networkInterfaces/loadBalancers/read|Obtém todos os balanceadores de carga Olá Olá interface de rede é parte de|
|/networkInterfaces/ipconfigurations/read|Obter uma definição de configuração de IP do adaptador de rede. |
|/publicIPAddresses/read|Obter uma definição de endereço IP público.|
|/publicIPAddresses/write|Criar um endereço IP público ou atualizar um endereço IP público existente. |
|/publicIPAddresses/delete|Excluir um endereço IP público.|
|/publicIPAddresses/join/action|Ingressar em um endereço IP público|
|/routeFilters/read|Obter uma definição de filtro de rota|
|/routeFilters/join/action|Ingressar em um filtro de rota|
|/routeFilters/delete|Excluir uma definição de filtro de rota|
|/routeFilters/write|Criar um filtro de rota ou atualizar um filtro de rota existente|
|/routeFilters/rules/read|Obter uma definição de regra de filtro de rota|
|/routeFilters/rules/write|Criar uma regra de filtro de rota ou atualizar uma regra de filtro de rota existente|
|/routeFilters/rules/delete|Excluir uma definição de regra de filtro de rota|
|/networkWatchers/read|Obter definição de Inspetor de rede Olá|
|/networkWatchers/write|Criar um observador de rede ou atualizar um observador de rede existente|
|/networkWatchers/delete|Excluir um observador de rede|
|/networkWatchers/configureFlowLog/action|Configurar o registro de fluxo em log para um recurso de destino.|
|/networkWatchers/ipFlowVerify/action|Retorna se o pacote de saudação é permitido ou negado tooor de um destino específico.|
|/networkWatchers/nextHop/action|Para um destino especificado e o endereço IP de destino, retornar o tipo de próximo salto hello e em seguida Esperamos que endereço IP.|
|/networkWatchers/queryFlowLogStatus/action|Obtém o status de saudação do fluxo de log em um recurso.|
|/networkWatchers/queryTroubleshootResult/action|Obtém a saudação resultados de saudação executada anteriormente ou executando a operação de solução de problemas de solução de problemas.|
|/networkWatchers/securityGroupView/action|Exibir hello configurado e regras de grupo de segurança de rede eficaz aplicadas em uma máquina virtual.|
|/networkWatchers/topology/action|Obter uma exibição dos recursos em nível de rede e de suas relações em um grupo de recursos.|
|/networkWatchers/troubleshoot/action|Iniciar a solução de problemas em um recurso de rede no Azure.|
|/networkWatchers/packetCaptures/queryStatus/action|Obter informações sobre propriedades e status de um recurso de captura de pacote.|
|/networkWatchers/packetCaptures/stop/action|Pare Olá que executa a sessão de captura de pacote.|
|/networkWatchers/packetCaptures/read|Obter definição de captura de pacote de saudação|
|/networkWatchers/packetCaptures/write|Criar uma captura de pacote|
|/networkWatchers/packetCaptures/delete|Excluir uma captura de pacote|
|/loadBalancers/read|Obter uma definição de balanceador de carga|
|/loadBalancers/write|Criar um balanceador de carga ou atualizar um balanceador de carga existente|
|/loadBalancers/delete|Excluir um balanceador de carga|
|/loadBalancers/networkInterfaces/read|Obtém referências de interfaces de rede Olá tooall sob o balanceador de carga|
|/loadBalancers/loadBalancingRules/read|Obter uma definição regra de balanceamento de carga do balanceador de carga|
|/loadBalancers/backendAddressPools/read|Obter uma definição de pool de endereços de back-end do balanceador de carga|
|/loadBalancers/backendAddressPools/join/action|Ingressar em um pool de endereços de back-end do balanceador de carga|
|/loadBalancers/inboundNatPools/read|Obter uma definição de pool NAT de entrada do balanceador de carga|
|/loadBalancers/inboundNatPools/join/action|Ingressar em um pool NAT de entrada do balanceador de carga|
|/loadBalancers/inboundNatRules/read|Obter uma definição de regra NAT de entrada do balanceador de carga|
|/loadBalancers/inboundNatRules/write|Criar uma regra NAT de entrada do balanceador de carga ou atualizar uma regra NAT de entrada do balanceador de carga existente|
|/loadBalancers/inboundNatRules/delete|Excluir uma regra NAT de entrada do balanceador de carga|
|/loadBalancers/inboundNatRules/join/action|Adicionar uma regra NAT de entrada do balanceador de carga|
|/loadBalancers/outboundNatRules/read|Obter uma definição de regra NAT de saída do balanceador de carga|
|/loadBalancers/probes/read|Obter uma investigação do balanceador de carga|
|/loadBalancers/virtualMachines/read|Obtém referências tooall Olá máquinas virtuais de um balanceador de carga|
|/loadBalancers/frontendIPConfigurations/read|Obter uma definição de configuração de IP de front-end do balanceador de carga|
|/trafficManagerGeographicHierarchies/read|Obtém Olá Traffic Manager geográfico hierarquia que contém regiões que podem ser usados com hello método de roteamento de tráfego geográfica|
|/bgpServiceCommunities/read|Obter comunidades do serviço BGP|
|/applicationGatewayAvailableWafRuleSets/read|Obter conjuntos de regras WAF disponíveis para o Gateway de Aplicativo|
|/virtualNetworks/read|Obter definição de rede virtual Olá|
|/virtualNetworks/write|Criar uma rede virtual ou atualizar uma rede virtual existente|
|/virtualNetworks/delete|Excluir uma rede virtual|
|/virtualNetworks/peer/action|Colocar uma rede virtual com outra rede virtual de mesmo nível|
|/virtualNetworks/virtualNetworkPeerings/read|Obter uma definição de emparelhamento de rede virtual|
|/virtualNetworks/virtualNetworkPeerings/write|Criar um emparelhamento de rede virtual ou atualizar um emparelhamento de rede virtual existente|
|/virtualNetworks/virtualNetworkPeerings/delete|Excluir um emparelhamento de redes virtuais|
|/virtualNetworks/subnets/read|Obter uma definição de sub-rede da rede virtual|
|/virtualNetworks/subnets/write|Criar uma sub-rede de rede virtual ou atualizar uma sub-rede de rede virtual existente|
|/virtualNetworks/subnets/delete|Excluir uma sub-rede de rede virtual|
|/virtualNetworks/subnets/join/action|Ingressar em uma rede virtual|
|/virtualNetworks/subnets/joinViaServiceTunnel/action|Une o recurso, como conta de armazenamento ou SQL tooa serviço encapsulamento habilitado sub-rede do banco de dados.|
|/virtualNetworks/subnets/virtualMachines/read|Obtém referências tooall Olá VMs em uma sub-rede de rede virtual|
|/virtualNetworks/checkIpAddressAvailability/read|Verifique se o endereço Ip está disponível na rede virtual especificado do hello|
|/virtualNetworks/virtualMachines/read|Obtém referências tooall Olá VMs em uma rede virtual|
|/expressRouteServiceProviders/read|Obter os provedores de serviços do ExpressRoute|
|/dnsoperationresults/read|Obter os resultados de uma operação de DNS|
|/localnetworkgateways/read|Obter o LocalNetworkGateway|
|/localnetworkgateways/write|Criar ou atualizar uma LocalNetworkGateway existente|
|/localnetworkgateways/delete|Excluir LocalNetworkGateway|
|/trafficManagerProfiles/read|Obter configuração de perfil do Traffic Manager hello. Isso inclui configurações DNS, configurações de roteamento de tráfego, configurações de monitoramento do ponto de extremidade e lista de saudação de pontos de extremidade roteados por este perfil do Gerenciador de tráfego.|
|/trafficManagerProfiles/write|Criar um perfil do Gerenciador de tráfego ou modificar a configuração de um perfil existente do Gerenciador de tráfego hello. Isso inclui habilitar ou desabilitar um perfil e modificar as configurações de DNS, configurações de roteamento de tráfego ou configurações de monitoramento do ponto de extremidade. Pontos de extremidade roteados pelo perfil do Traffic Manager Olá podem ser adicionados, removidos, habilitados ou desabilitados.|
|/trafficManagerProfiles/delete|Exclua perfil do Gerenciador de tráfego de saudação. Todas as configurações associadas Olá perfil do Gerenciador de tráfego serão perdidas e perfil de saudação não pode mais ser usado tooroute tráfego.|
|/dnsoperationstatuses/read|Obter o status de uma operação de DNS |
|/operations/read|Obter operações disponíveis|
|/expressRouteCircuits/read|Obter um ExpressRouteCircuit|
|/expressRouteCircuits/write|Criar ou atualizar um ExpressRouteCircuit existente|
|/expressRouteCircuits/delete|Excluir um ExpressRouteCircuit|
|/expressRouteCircuits/stats/read|Obter status de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/read|Obter um emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/write|Criar ou atualizar um emparelhamento de ExpressRouteCircuit existente|
|/expressRouteCircuits/peerings/delete|Excluir um emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/arpTables/action|Obter ArpTable de emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/routeTables/action|Obter RouteTable de emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/<br>routeTablesSummary/action|Obter um resumo de RouteTable de emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/peerings/stats/read|Obter status de emparelhamento de ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/read|Obter uma autorização ExpressRouteCircuit|
|/expressRouteCircuits/authorizations/write|Criar ou atualizar uma autorização ExpressRouteCircuit existente|
|/expressRouteCircuits/authorizations/delete|Excluir uma autorização ExpressRouteCircuit|
|/connections/read|Obter o VirtualNetworkGatewayConnection|
|/connections/write|Criar ou atualizar uma VirtualNetworkGatewayConnection existente|
|/connections/delete|Excluir VirtualNetworkGatewayConnection|
|/connections/sharedKey/read|Obter SharedKey da VirtualNetworkGatewayConnection|
|/connections/sharedKey/write|Criar ou atualizar uma VirtualNetworkGatewayConnection SharedKey existente|
|/networkSecurityGroups/read|Obter uma definição de um grupo de segurança de rede|
|/networkSecurityGroups/write|Criar um grupo de segurança de rede ou atualizar um grupo de segurança de rede existente|
|/networkSecurityGroups/delete|Excluir um grupo de segurança de rede|
|/networkSecurityGroups/join/action|Ingressar em um grupo de segurança de rede|
|/networkSecurityGroups/defaultSecurityRules/read|Obter uma definição padrão da regra de segurança|
|/networkSecurityGroups/securityRules/read|Obter uma definição da regra de segurança|
|/networkSecurityGroups/securityRules/write|Criar uma regra de segurança ou atualizar uma regra de segurança existente|
|/networkSecurityGroups/securityRules/delete|Excluir uma regra de segurança|
|/applicationGateways/read|Obter um gateway de aplicativo|
|/applicationGateways/write|Criar ou atualizar um gateway de aplicativo|
|/applicationGateways/delete|Excluir um gateway de aplicativo|
|/applicationGateways/backendhealth/action|Obter uma integridade de back-end do Gateway de Aplicativo|
|/applicationGateways/start/action|Inicia um gateway de aplicativo|
|/applicationGateways/stop/action|Interrompe um gateway de aplicativo|
|/applicationGateways/backendAddressPools/join/action|Ingressar em um pool de endereços de back-end do gateway de aplicativo|
|/routeTables/read|Obter uma definição de tabela de rota|
|/routeTables/write|Criar uma tabela de rotas ou atualizar uma tabela de rotas existente|
|/routeTables/delete|Excluir uma definição de tabela de rota|
|/routeTables/join/action|Ingressar em uma tabela de rotas|
|/routeTables/routes/read|Obter uma definição de rota|
|/routeTables/routes/write|Criar uma rota ou atualizar uma rota existente|
|/routeTables/routes/delete|Excluir uma definição de rota|
|/locations/operationResults/read|Obter o resultado de uma operação POST ou DELETE assíncrona|
|/locations/checkDnsNameAvailability/read|Verifica se o rótulo dns está disponível em Olá especificado local|
|/locations/usages/read|Obtém as métricas de uso de recursos de saudação|
|/locations/operations/read|Obter o recurso de operação que representa o status de uma operação assíncrona|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de NotifciationHubs hello e permite a criação de saudação de Namespaces e NotificationHubs|
|/CheckNamespaceAvailability/action|Verifica se um determinado nome de recurso do Namespace está disponível no hello serviço do NotificationHub.|
|/Namespaces/write|Criar um recurso de namespace e atualizar suas propriedades. Marcações e status do Namespace de saudação são propriedades de saudação que podem ser atualizadas.|
|/Namespaces/read|Obter lista de saudação da descrição do recurso de Namespace|
|/Namespaces/Delete|Excluir o recurso de namespace|
|/Namespaces/authorizationRules/action|Obter lista de saudação da descrição de regras de autorização de Namespaces.|
|/Namespaces/CheckNotificationHubAvailability/action|Verificar se determinado nome de NotificationHub está disponível em um Namespace.|
|/Namespaces/authorizationRules/write|Criar regras de autorização no nível do namespace e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/Namespaces/authorizationRules/read|Obter lista de saudação da descrição de regras de autorização de Namespaces.|
|/Namespaces/authorizationRules/delete|Excluir regra de autorização de namespace. saudação de regra de autorização de Namespace padrão não pode ser excluída. |
|/Namespaces/authorizationRules/listkeys/action|Obter cadeia de caracteres de Conexão de saudação toohello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/action|Namespace autorização regra regenerar primária/chave secundária, especifique Olá chave que precisa toobe regenerado|
|/Namespaces/NotificationHubs/write|Criar um Hub de notificação e atualizar suas propriedades. Suas propriedades incluem principalmente as credenciais PNS. Tempo de vida útil e regras de autorização|
|/Namespaces/NotificationHubs/read|Obter lista de descrições de recursos do Hub de notificação|
|/Namespaces/NotificationHubs/Delete|Excluir recurso de Hub de notificação|
|/Namespaces/NotificationHubs/authorizationRules/action|Obter lista de saudação de regras de autorização do Hub de notificação|
|/Namespaces/NotificationHubs/pnsCredentials/action|Obter todas as credenciais PNS do Hub de notificação. Isso inclui credenciais WNS, MPNS, APNS, GCM e Baidu|
|/Namespaces/NotificationHubs/debugSend/action|Enviar notificação por push de teste.|
|/Namespaces/NotificationHubs/metricDefinitions/read|Obter lista de métrica de descrições de recurso de métrica do namespace|
|/Namespaces/NotificationHubs/<br>authorizationRules/write|Criar regras de autorização do Hub de notificação e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/Namespaces/NotificationHubs/<br>authorizationRules/read|Obter lista de saudação de regras de autorização do Hub de notificação|
|/Namespaces/NotificationHubs/<br>authorizationRules/delete|Excluir regras de autorização do Hub de notificação|
|/Namespaces/NotificationHubs/<br>authorizationRules/listkeys/action|Obter cadeia de caracteres de Conexão de saudação toohello Hub de notificação|
|/Namespaces/NotificationHubs/<br>authorizationRules/regenerateKeys/action|Notificação de Hub autorização regra regenerar primária/chave secundária, especifique Olá chave que precisa toobe regenerada|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Operação | Descrição |
|---|---|
|/register/action|Registre um provedor de recursos de tooa de assinatura.|
|/linkTargets/read|Listar as contas existentes que não estão associadas uma assinatura do Azure. toolink este espaço de trabalho de tooa de assinatura do Azure, use uma id de cliente retornados por esta operação na propriedade de id de cliente de saudação do Olá operação criar espaço de trabalho.|
|/workspaces/write|Cria um novo espaço de trabalho ou o espaço de trabalho existente do tooan links, fornecendo a id de cliente de saudação do espaço de trabalho existente do hello.|
|/workspaces/read|Obter um espaço de trabalho existente|
|/workspaces/delete|Excluir um espaço de trabalho. Se o espaço de trabalho de saudação foi vinculado tooan o espaço de trabalho existente no momento da criação, em seguida, Olá foi vinculado toois não excluído do espaço de trabalho.|
|/workspaces/generateregistrationcertificate/action|Gera de registro de certificado para o espaço de trabalho de saudação. Esse certificado é usado tooconnect Microsoft System Center Operation Manager toohello espaço de trabalho.|
|/workspaces/sharedKeys/action|Recupera as chaves do espaço de trabalho de saudação Olá compartilhado. Essas chaves são usadas tooconnect Insights operacionais do Microsoft agentes toohello espaço de trabalho.|
|/workspaces/search/action|Executar uma consulta de pesquisa|
|/workspaces/datasources/read|Obter fontes de dados em um espaço de trabalho.|
|/workspaces/datasources/write|Criar/atualizar fontes de dados em um espaço de trabalho.|
|/workspaces/datasources/delete|Excluir fontes de dados em um espaço de trabalho.|
|/workspaces/managementGroups/read|Obtém o hello nomes e metadados para o espaço de trabalho do System Center Operations Manager gerenciamento grupos toothis conectado.|
|/workspaces/schema/read|Obtém o esquema de pesquisa de saudação do espaço de trabalho de saudação.  Esquema de pesquisa inclui Olá exposto campos e seus tipos.|
|/workspaces/usages/read|Obtém dados de uso de um espaço de trabalho incluindo Olá quantidade de dados lidos por espaço de trabalho de saudação.|
|/workspaces/intelligencepacks/read|Lista todos os pacotes de inteligência que estão visíveis para um determinado espaço de trabalho e também indica se o pacote de saudação está habilitada ou desabilitada para esse espaço de trabalho.|
|/workspaces/intelligencepacks/enable/action|Habilitar um pacote de inteligência para determinado espaço de trabalho.|
|/workspaces/intelligencepacks/disable/action|Desabilitar um pacote de inteligência para determinado espaço de trabalho.|
|/workspaces/sharedKeys/read|Recupera as chaves do espaço de trabalho de saudação Olá compartilhado. Essas chaves são usadas tooconnect Insights operacionais do Microsoft agentes toohello espaço de trabalho.|
|/workspaces/savedSearches/read|Obter uma consulta de pesquisa salva|
|/workspaces/savedSearches/write|Criar uma consulta de pesquisa salva|
|/workspaces/savedSearches/delete|Excluir uma consulta de pesquisa salva|
|/workspaces/storageinsightconfigs/write|Criar uma nova configuração de armazenamento. Essas configurações são usadas toopull dados de um local em uma conta de armazenamento existente.|
|/workspaces/storageinsightconfigs/read|Obter uma configuração de armazenamento.|
|/workspaces/storageinsightconfigs/delete|Excluir uma configuração de armazenamento. Isso interromperá a Insights operacionais do Microsoft leiam os dados da conta de armazenamento hello.|
|/workspaces/configurationScopes/read|Obter escopo de configuração|
|/workspaces/configurationScopes/write|Definir o escopo da configuração|
|/workspaces/configurationScopes/delete|Excluir escopo de configuração|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Operação | Descrição |
|---|---|
|/register/action|Registre um provedor de recursos de tooa de assinatura.|
|/solutions/write|Criar nova solução do OMS|
|/solutions/read|Obter solução OMS de saída|
|/solutions/delete|Excluir a solução do OMS existente|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Operação | Descrição |
|---|---|
|/Vaults/backupJobsExport/action|Exportar trabalhos|
|/Vaults/write|A operação Criar cofre cria um recurso do Azure do tipo 'cofre'|
|/Vaults/read|Olá operação obter cofre obtém um objeto que representa a saudação recursos do Azure do tipo 'cofre'|
|/Vaults/delete|Olá Olá de exclusões de operação Excluir cofre especificado recursos do Azure do tipo 'cofre'|
|/Vaults/refreshContainers/read|Atualiza a lista de contêineres de saudação|
|/Vaults/backupJobsExport/operationResults/read|Olá retorna resultados da operação de trabalho de exportação.|
|/Vaults/backupOperationResults/read|Retornar o resultado da operação de backup para o cofre dos Serviços de Recuperação.|
|/Vaults/monitoringAlerts/read|Obtém os alertas de saudação para Cofre de serviços de recuperação de saudação.|
|/Vaults/monitoringAlerts/{uniqueAlertId}/read|Obtém os detalhes de saudação do alerta de saudação.|
|/Vaults/backupSecurityPIN/read|Retornar a informação de PIN de segurança para o cofre dos Serviços de Recuperação.|
|/vaults/replicationEvents/read|Ler eventos|
|/Vaults/backupProtectableItems/read|Retornar a lista de todos os itens que podem ser protegidos.|
|/vaults/replicationFabrics/read|Ler malhas|
|/vaults/replicationFabrics/write|Criar ou atualizar malhas|
|/vaults/replicationFabrics/remove/action|Remover malha|
|/vaults/replicationFabrics/checkConsistency/action|Verificações de consistência de saudação do Fabric|
|/vaults/replicationFabrics/delete|Excluir malhas|
|/vaults/replicationFabrics/renewcertificate/action||
|/vaults/replicationFabrics/deployProcessServerImage/action|Implantar imagem do servidor de processo|
|/vaults/replicationFabrics/reassociateGateway/action|Reassociar gateway|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>leitura|Ler provedores de serviços de recuperação|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>remove/action|Remover o provedor dos Serviços de Recuperação|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>excluir|Excluir provedor dos Serviços de Recuperação|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>refreshProvider/action|Atualizar provedor|
|/vaults/replicationFabrics/replicationStorageClassifications/read|Ler classificações de armazenamento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/read|Ler mapeamentos de classificação de armazenamento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/write|Criar ou atualizar os mapeamentos de classificação de armazenamento|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/delete|Excluir mapeamentos de classificação de armazenamento|
|/vaults/replicationFabrics/replicationvCenters/read|Ler todos os trabalhos|
|/vaults/replicationFabrics/replicationvCenters/write|Criar ou atualizar os trabalhos|
|/vaults/replicationFabrics/replicationvCenters/delete|Excluir trabalhos|
|/vaults/replicationFabrics/replicationNetworks/read|Ler redes|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/read|Ler mapeamentos de rede|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/write|Criar ou atualizar os mapeamentos de rede|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/delete|Excluir mapeamentos de rede|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>leitura|Ler contêineres de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>discoverProtectableItem/action|Descobrir item que pode ser protegido|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>gravação|Criar ou atualizar contêineres de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>remove/action|Remover o contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>switchprotection/action|Alterar contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectableItems/read|Ler itens que podem ser protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/read|Ler mapeamentos de contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/write|Criar ou atualizar os mapeamentos de contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/remove/action|Remover o mapeamento de contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/delete|Excluir mapeamentos de contêiner de proteção|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/read|Ler itens protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/write|Criar ou atualizar os itens protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/delete|Excluir itens protegidos|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/remove/action|Remover item protegido|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/plannedFailover/action|Failover planejado|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/unplannedFailover/action|Failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailover/action|Failover de Teste|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailoverCleanup/action|Limpeza do Failover de teste|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/failoverCommit/action|Confirmação de failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/reProtect/action|Proteger item protegido novamente|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/updateMobilityService/action|Atualizar serviço de mobilidade|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/repairReplication/action|Reparar replicação|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/applyRecoveryPoint/action|Aplicar ponto de recuperação|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/recoveryPoints/read|Ler pontos de recuperação de replicação|
|/vaults/replicationPolicies/read|Ler políticas|
|/vaults/replicationPolicies/write|Criar ou atualizar as políticas|
|/vaults/replicationPolicies/delete|Excluir políticas|
|/vaults/replicationRecoveryPlans/read|Ler planos de recuperação|
|/vaults/replicationRecoveryPlans/write|Criar ou atualizar planos de recuperação|
|/vaults/replicationRecoveryPlans/delete|Excluir planos de recuperação|
|/vaults/replicationRecoveryPlans/plannedFailover/action|Plano de recuperação de failover planejado|
|/vaults/replicationRecoveryPlans/unplannedFailover/action|Plano de recuperação de failover|
|/vaults/replicationRecoveryPlans/testFailover/action|Testar plano de recuperação de failover|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/action|Testar plano de recuperação de limpeza do failover|
|/vaults/replicationRecoveryPlans/failoverCommit/action|Plano de recuperação de confirmação de failover|
|/vaults/replicationRecoveryPlans/reProtect/action|Proteja plano de recuperação novamente|
|/Vaults/extendedInformation/read|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/Vaults/extendedInformation/write|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/Vaults/extendedInformation/delete|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/Vaults/backupManagementMetaData/read|Retornar metadados de gerenciamento de backup para o cofre dos Serviços de Recuperação.|
|/Vaults/backupProtectionContainers/read|Retorna todos os contêineres pertencentes toohello assinatura|
|/Vaults/backupFabrics/operationResults/read|Retorna o status da operação de saudação|
|/Vaults/backupFabrics/protectionContainers/read|Retornar todos os contêineres registrados|
|/Vaults/backupFabrics/protectionContainers/<br>operationResults/read|Obter o resultado da operação executada no contêiner de proteção.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/read|Retorna os detalhes do Item protegido de saudação objeto|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/write|Criar um item protegido de backup|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/delete|Excluir item protegido|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/backup/action|Executar um backup para um item protegido.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationResults/read|Obter o resultado da operação executada em itens protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationStatus/read|Retorna o status de saudação da operação executada em itens protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/read|Obter pontos de recuperação para itens protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>restore/action|Restaurar pontos de recuperação para itens protegidos.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>provisionInstantItemRecovery/action|Provisionar recuperação de item instantânea para item protegido|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>revokeInstantItemRecovery/action|Revogar a recuperação de item instantânea para item protegido|
|/Vaults/usages/read|Retornar os detalhes de uso para um cofre dos Serviços de Recuperação.|
|/vaults/usages/read|Ler usos de cofre|
|/Vaults/certificates/write|Olá a operação de certificado do recurso de atualização atualiza o certificado de credencial de cofre/recurso hello.|
|/Vaults/tokenInfo/read|Retornar a informação de token para o cofre dos Serviços de Recuperação.|
|/vaults/replicationAlertSettings/read|Ler configurações de alertas|
|/vaults/replicationAlertSettings/write|Criar ou atualizar as configurações de alertas|
|/Vaults/backupOperations/read|Retornar o status da operação de backup para o cofre dos Serviços de Recuperação.|
|/Vaults/storageConfig/read|Retornar cofre de armazenamento para o cofre dos Serviços de Recuperação.|
|/Vaults/storageConfig/write|Atualizar cofre de armazenamento para o cofre dos Serviços de Recuperação.|
|/Vaults/backupUsageSummaries/read|Retornar resumos de itens protegidos e servidores protegidos para os Serviços de Recuperação.|
|/Vaults/backupProtectedItems/read|Retorna Olá lista de todos os itens protegidos.|
|/Vaults/backupconfig/vaultconfig/read|Retornar a configuração para cofre dos Serviços de Recuperação.|
|/Vaults/backupconfig/vaultconfig/write|Atualizar configuração para o cofre dos Serviços de Recuperação.|
|/Vaults/registeredIdentities/write|Olá operação registrar contêiner de serviço pode ser usado tooregister um contêiner com o serviço de recuperação.|
|/Vaults/registeredIdentities/read|Olá obter contêineres pode ser usada a operação obter contêineres de saudação registrados para um recurso.|
|/Vaults/registeredIdentities/delete|Olá operação Cancelar registro do contêiner pode ser usado toounregister um contêiner.|
|/Vaults/registeredIdentities/operationResults/read|Olá operação obter resultados da operação pode ser usada para obter status da operação hello e resultar de saudação assincronamente enviada operação|
|/vaults/replicationJobs/read|Ler todos os trabalhos|
|/vaults/replicationJobs/cancel/action|Cancelar trabalho|
|/vaults/replicationJobs/restart/action|Reiniciar o trabalho|
|/vaults/replicationJobs/resume/action|Retomar o trabalho|
|/Vaults/backupPolicies/read|Retornar todas as políticas de proteção|
|/Vaults/backupPolicies/write|Criar uma política de proteção|
|/Vaults/backupPolicies/delete|Excluir uma política de proteção|
|/Vaults/backupPolicies/operationResults/read|Obter os resultados da operação de política.|
|/Vaults/backupPolicies/operationStatus/read|Obter o status da operação de política.|
|/Vaults/vaultTokens/read|Olá operação do Token do cofre pode ser usado tooget de Token do cofre para operações de nível de back-end do cofre.|
|/Vaults/monitoringConfigurations/notificationConfiguration/read|Obtém a configuração de notificação do hello recuperação serviços cofre.|
|/Vaults/backupJobs/read|Retornar todos os objetos de trabalho|
|/Vaults/backupJobs/cancel/action|Olá Cancelar trabalho|
|/Vaults/backupJobs/operationResults/read|Olá retorna resultado da operação do trabalho.|
|/locations/allocateStamp/action|AllocateStamp é uma operação interna usada pelo serviço|
|/locations/allocatedStamp/read|GetAllocatedStamp é uma operação interna usada pelo serviço|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Operação | Descrição |
|---|---|
|/checkNamespaceAvailability/action|Verificar a disponibilidade do namespace em determinada assinatura.|
|/register/action|Registra a assinatura Olá para o provedor de recursos de retransmissão hello e permite a criação de saudação de recursos de retransmissão|
|/namespaces/write|Criar um recurso de namespace e atualizar suas propriedades. Marcações e status do Namespace de saudação são propriedades de saudação que podem ser atualizadas.|
|/namespaces/read|Obter lista de saudação da descrição do recurso de Namespace|
|/namespaces/Delete|Excluir o recurso de namespace|
|/namespaces/authorizationRules/write|Criar regras de autorização no nível do namespace e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/authorizationRules/delete|Excluir regra de autorização de namespace. saudação de regra de autorização de Namespace padrão não pode ser excluída. |
|/namespaces/authorizationRules/listkeys/action|Obter cadeia de caracteres de Conexão de saudação toohello Namespace|
|/namespaces/HybridConnections/write|Criar ou atualizar propriedades HybridConnection.|
|/namespaces/HybridConnections/read|Obter lista de descrições de recursos HybridConnection|
|/namespaces/HybridConnections/Delete|Toodelete operação recurso HybridConnection|
|/namespaces/HybridConnections/authorizationRules/write|Criar regras de autorização HybridConnection e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/HybridConnections/authorizationRules/delete|Operação toodelete HybridConnection as regras de autorização|
|/namespaces/HybridConnections/authorizationRules/listkeys/action|Obter Olá tooHybridConnection de cadeia de caracteres de Conexão|
|/namespaces/WcfRelays/write|Criar ou atualizar propriedades WcfRelay.|
|/namespaces/WcfRelays/read|Obter lista de descrições de recursos WcfRelay|
|/namespaces/WcfRelays/Delete|Toodelete operação recurso WcfRelay|
|/namespaces/WcfRelays/authorizationRules/write|Criar regras de autorização WcfRelay e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/WcfRelays/authorizationRules/delete|Operação toodelete WcfRelay as regras de autorização|
|/namespaces/WcfRelays/authorizationRules/listkeys/action|Obter Olá tooWcfRelay de cadeia de caracteres de Conexão|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Operação | Descrição |
|---|---|
|/AvailabilityStatuses/read|Obtém status de disponibilidade Olá para todos os recursos Olá especificado escopo|
|/AvailabilityStatuses/current/read|Obtém status de disponibilidade Olá para Olá o recurso especificado|

## <a name="microsoftresources"></a>Microsoft.Resources

| Operação | Descrição |
|---|---|
|/checkResourceName/action|Verifique o nome de recurso de saudação de validade.|
|/providers/read|Obter lista de saudação de provedores.|
|/subscriptions/read|Obtém a lista de saudação de assinaturas.|
|/subscriptions/operationresults/read|Obter assinatura Olá resultados da operação.|
|/subscriptions/providers/read|Obter ou listar provedores de recursos.|
|/subscriptions/tagNames/read|Obter ou listar marcações de assinatura.|
|/subscriptions/tagNames/write|Adicionar uma marcação de assinatura.|
|/subscriptions/tagNames/delete|Excluir uma marcação de assinatura.|
|/subscriptions/tagNames/tagValues/read|Obter ou listar valores de marcação de assinatura.|
|/subscriptions/tagNames/tagValues/write|Adicionar um valor de marcação de assinatura.|
|/subscriptions/tagNames/tagValues/delete|Excluir um valor de marcação de assinatura.|
|/subscriptions/resources/read|Obter os recursos de uma assinatura.|
|/subscriptions/resourceGroups/read|Obter ou listar de grupos de recursos.|
|/subscriptions/resourceGroups/write|Criar ou atualizar um grupo de recursos.|
|/subscriptions/resourceGroups/delete|Excluir um grupo de recursos e todos os seus recursos.|
|/subscriptions/resourceGroups/moveResources/action|Move recursos de um recurso grupo tooanother.|
|/subscriptions/resourceGroups/validateMoveResources/action|Valide movimentação de recursos de um recurso grupo tooanother.|
|/subscriptions/resourcegroups/resources/read|Obtém recursos Olá Olá para grupo de recursos.|
|/subscriptions/resourcegroups/deployments/read|Obter ou lista implantações.|
|/subscriptions/resourcegroups/deployments/write|Criar ou atualizar uma implantação.|
|/subscriptions/resourcegroups/deployments/operationstatuses/read|Obter ou listar o status da operação de implantação.|
|/subscriptions/resourcegroups/deployments/operations/read|Obter ou lista operações de implantação.|
|/subscriptions/locations/read|Obtém a lista de saudação de locais com suporte.|
|/links/read|Obter ou listar links de recursos.|
|/links/write|Criar ou atualizar um link de recurso.|
|/links/delete|Excluir um link de recurso.|
|/tenants/read|Obtém a lista de saudação de locatários.|
|/resources/read|Obter lista de saudação de recursos com base em filtros.|
|/deployments/read|Obter ou lista implantações.|
|/deployments/write|Criar ou atualizar uma implantação.|
|/deployments/delete|Excluir uma implantação.|
|/deployments/cancel/action|Cancelar uma implantação.|
|/deployments/validate/action|Validar uma implantação.|
|/deployments/operations/read|Obter ou lista operações de implantação.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Operação | Descrição |
|---|---|
|/jobcollections/read|Obter coleção de trabalhos|
|/jobcollections/write|Criar ou atualizar a coleção de trabalhos.|
|/jobcollections/delete|Excluir coleção de trabalhos.|
|/jobcollections/enable/action|Habilita coleção de trabalhos.|
|/jobcollections/disable/action|Desabilita coleção de trabalhos.|
|/jobcollections/jobs/read|Obter o trabalho.|
|/jobcollections/jobs/write|Criar ou atualizar o trabalho.|
|/jobcollections/jobs/delete|Excluir trabalho.|
|/jobcollections/jobs/run/action|Executa o trabalho.|
|/jobcollections/jobs/generateLogicAppDefinition/action|Gerar a definição de aplicativo lógico com base em um trabalho do Agendador.|
|/jobcollections/jobs/jobhistories/read|Obtém o histórico de trabalhos.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de pesquisa hello e permite a criação de saudação de serviços de pesquisa.|
|/checkNameAvailability/action|Verifica a disponibilidade do nome do serviço hello.|
|/searchServices/write|Cria ou atualiza o serviço de pesquisa de saudação.|
|/searchServices/read|Lê o serviço de pesquisa de saudação.|
|/searchServices/delete|Exclui o serviço de pesquisa de saudação.|
|/searchServices/start/action|Inicia o serviço de pesquisa de saudação.|
|/searchServices/stop/action|Interrompe o serviço de pesquisa hello.|
|/searchServices/listAdminKeys/action|Lê as chaves de administração de saudação.|
|/searchServices/regenerateAdminKey/action|Regenera a chave de administração de saudação.|
|/searchServices/createQueryKey/action|Cria a chave de consulta hello.|
|/searchServices/queryKey/read|Lê as chaves de consulta hello.|
|/searchServices/queryKey/delete|Exclui a chave de consulta hello.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Operação | Descrição |
|---|---|
|/jitNetworkAccessPolicies/read|Obtém as políticas de acesso de rede just-in-time Olá|
|/jitNetworkAccessPolicies/write|Criar uma nova política de acesso de rede just-in-time ou atualizar uma existente|
|/jitNetworkAccessPolicies/initiate/action|Iniciar uma política de acesso de rede just-in-time|
|/securitySolutionsReferenceData/read|Obtém os dados de referência de soluções de segurança Olá|
|/securityStatuses/read|Obtém status de integridade de segurança Olá para recursos do Azure|
|/webApplicationFirewalls/read|Obtém os firewalls de aplicativo web Olá|
|/webApplicationFirewalls/write|Criar um novo firewall do aplicativo Web ou atualizar um existente|
|/webApplicationFirewalls/delete|Excluir um firewall do aplicativo Web|
|/securitySolutions/read|Obtém as soluções de segurança de saudação|
|/securitySolutions/write|Criar uma nova solução de segurança ou atualizar uma existente|
|/securitySolutions/delete|Excluir uma solução de segurança|
|/tasks/read|Obter todas as recomendações de segurança disponíveis|
|/tasks/dismiss/action|Ignorar recomendação de segurança|
|/tasks/activate/action|Ativar recomendação de segurança|
|/policies/read|Obtém a política de segurança de saudação|
|/policies/write|Olá de atualizações de política de segurança|
|/applicationWhitelistings/read|Obtém a saudação aplicativo whitelistings|
|/applicationWhitelistings/write|Criar uma nova lista de exceções do aplicativo ou atualizar uma existente|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Operação | Descrição |
|---|---|
|/subscriptions/write|Criar ou atualizar uma assinatura|
|/gateways/write|Criar ou atualizar um gateway|
|/gateways/delete|Excluir um gateway|
|/gateways/read|Obter um gateway|
|/gateways/regenerateprofile/action|Gera novamente o perfil de gateway Olá|
|/gateways/upgradetolatest/action|Versão mais recente do toohello atualizações Olá gateway|
|/nodes/write|criar ou atualizar um nó|
|/nodes/delete|Excluir um nó|
|/nodes/read|Obter um nó|
|/sessions/write|Criar ou atualizar uma sessão|
|/sessions/read|Obter uma sessão|
|/sessions/delete|Excluir uma sessão|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Operação | Descrição |
|---|---|
|/checkNameAvailability/action|Verificar a disponibilidade do namespace em determinada assinatura.|
|/register/action|Registra a assinatura Olá para o provedor de recursos do ServiceBus hello e permite a criação de saudação do barramento de serviço de recursos|
|/namespaces/write|Criar um recurso de namespace e atualizar suas propriedades. Marcações e status do Namespace de saudação são propriedades de saudação que podem ser atualizadas.|
|/namespaces/read|Obter lista de saudação da descrição do recurso de Namespace|
|/namespaces/Delete|Excluir o recurso de namespace|
|/namespaces/metricDefinitions/read|Obter lista de métrica de descrições de recurso de métrica do namespace|
|/namespaces/authorizationRules/write|Criar regras de autorização no nível do namespace e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/authorizationRules/read|Obter lista de saudação da descrição de regras de autorização de Namespaces.|
|/namespaces/authorizationRules/delete|Excluir regra de autorização de namespace. saudação de regra de autorização de Namespace padrão não pode ser excluída. |
|/namespaces/authorizationRules/listkeys/action|Obter cadeia de caracteres de Conexão de saudação toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Regenerar Olá primário ou secundário chave toohello recursos|
|/namespaces/diagnosticSettings/read|Obter lista de descrições de recurso de configurações de diagnóstico do namespace|
|/namespaces/diagnosticSettings/write|Obter lista de descrições de recurso de configurações de diagnóstico do namespace|
|/namespaces/queues/write|Criar ou atualizar propriedades Queue.|
|/namespaces/queues/read|Obter lista de descrições do recurso Queue|
|/namespaces/queues/Delete|Toodelete operação recurso de fila|
|/namespaces/queues/authorizationRules/write|Criar regras de autorização de fila e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/queues/authorizationRules/read| Obter lista de saudação de regras de autorização de fila|
|/namespaces/queues/authorizationRules/delete|Operação toodelete regras de autorização de fila|
|/namespaces/queues/authorizationRules/listkeys/action|Obter Olá tooQueue de cadeia de caracteres de Conexão|
|/namespaces/queues/authorizationRules/regenerateKeys/action|Regenerar Olá primário ou secundário chave toohello recursos|
|/namespaces/logDefinitions/read|Obter lista de descrições do recurso de log do namespace|
|/namespaces/topics/write|Criar ou atualizar propriedades Topic.|
|/namespaces/topics/read|Obter lista de descrições de recurso Topic|
|/namespaces/topics/Delete|Toodelete operação recurso do tópico|
|/namespaces/topics/authorizationRules/write|Criar regras de autorização do tópico e atualizar suas propriedades. Olá direitos de acesso de regras de autorização, Olá primário e secundário chaves podem ser atualizadas.|
|/namespaces/topics/authorizationRules/read| Obter lista de saudação de regras de autorização do tópico|
|/namespaces/topics/authorizationRules/delete|Operação toodelete regras de autorização do tópico|
|/namespaces/topics/authorizationRules/listkeys/action|Obter Olá tooTopic de cadeia de caracteres de Conexão|
|/namespaces/topics/authorizationRules/regenerateKeys/action|Regenerar Olá primário ou secundário chave toohello recursos|
|/namespaces/topics/subscriptions/write|Criar ou atualizar propriedades TopicSubscription.|
|/namespaces/topics/subscriptions/read|Obter lista de descrições do recurso TopicSubscription|
|/namespaces/topics/subscriptions/Delete|Toodelete operação recurso TopicSubscription|
|/namespaces/topics/subscriptions/rules/write|Criar ou atualizar propriedades Rule.|
|/namespaces/topics/subscriptions/rules/read|Obter lista de descrições do recurso Rule|
|/namespaces/topics/subscriptions/rules/Delete|Toodelete operação recurso de regra|

## <a name="microsoftsql"></a>Microsoft.Sql

| Operação | Descrição |
|---|---|
|/servers/read|Retornar uma lista de servidores em um grupo de recursos de uma assinatura|
|/servers/write|Criar um novo servidor ou modificar propriedades de servidor existente em um grupo de recursos de uma assinatura|
|/servers/delete|Excluir um servidor e todos os bancos de dados e pools elásticos contidos|
|/servers/import/action|Criar um novo banco de dados no servidor de saudação e implantar o esquema e os dados de um pacote de DacPac|
|/servers/upgrade/action|Habilitar a nova funcionalidade disponível na versão mais recente de saudação do servidor e especificar o mapa de conversão de edição de bancos de dados|
|/servers/VulnerabilityAssessmentScans/action|Executar verificação de servidor para avaliação de vulnerabilidade|
|/servers/operationResults/read|Operação é usada tootrack progresso de atualização do servidor do toohigher de versão inferior|
|/servers/operationResults/delete|Anular a atualização de versão do servidor em andamento|
|/servers/securityAlertPolicies/read|Recuperar detalhes da política de detecção de ameaças Olá servidor configurado em um determinado servidor|
|/servers/securityAlertPolicies/write|Alterar a detecção de ameaças Olá server para um determinado servidor|
|/servers/securityAlertPolicies/operationResults/read|Recuperar os resultados do servidor de saudação operação de definição de política de detecção de ameaças|
|/servers/administrators/read|Recuperar detalhes do administrador do servidor|
|/servers/administrators/write|Criar ou atualizar o administrador do servidor|
|/servers/administrators/delete|Excluir o administrador do servidor do servidor de saudação|
|/servers/recoverableDatabases/read|Esta operação é usada para recuperação de desastres do banco de dados ao vivo toorestore banco de dados toolast conhecido bom ponto de backup. Retorna informações sobre Olá último backup, mas ele, na verdade, não restaure o banco de dados de saudação.|
|/servers/serviceObjectives/read|Recuperar a lista de objetivos de nível de serviço (também conhecido como níveis de desempenho) disponíveis em determinado servidor|
|/servers/firewallRules/read|Recuperar detalhes de regra de firewall do servidor|
|/servers/firewallRules/write|Criar ou atualizar regra de firewall de servidor que controla o intervalo de endereços IP permitidos tooconnect toohello server|
|/servers/firewallRules/delete|Excluir regra de firewall do servidor de saudação|
|/servers/administratorOperationResults/read|Recuperar resultados de operação do administrador do servidor|
|/servers/recommendedElasticPools/read|Recuperar uma recomendação para o banco de dados Elástico pools tooreduce custo ou melhorar o desempenho com base na utilização de recursos de historica|
|/servers/recommendedElasticPools/metrics/read|Recuperar a métrica de pools de banco de dados elástico recomendados para determinado servidor|
|/servers/recommendedElasticPools/databases/read|Recuperar bancos de dados que devem ser adicionados a pools de banco de dados elásticos recomendados para determinado servidor|
|/servers/elasticPools/read|Recuperar detalhes do pool de banco de dados elástico em determinado servidor|
|/servers/elasticPools/write|Criar um novo pool de banco de dados elástico ou alterar as propriedades de um existente|
|/servers/elasticPools/delete|Excluir pool de banco de dados elástico existente|
|/servers/elasticPools/operationResults/read|Recuperar detalhes sobre determinada operação de pool de banco de dados elástico|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/read|Retornar tipos de métricas que estão disponíveis para pools de bancos de dados elásticos|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtém a configuração de diagnóstico de saudação para o recurso de saudação|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/write|Cria ou atualiza a configuração de diagnóstico de saudação para o recurso de saudação|
|/servers/elasticPools/metrics/read|Retornar métrica de utilização de recursos do pool de banco de dados elástico|
|/servers/elasticPools/elasticPoolDatabaseActivity/read|Recuperar atividades e detalhes em um banco de dados que faz parte do pool de banco de dados elástico|
|/servers/elasticPools/advisors/read|Retorna a lista de supervisores disponíveis para o pool Elástico Olá|
|/servers/elasticPools/advisors/write|Atualizar status de execução automática de um assistente no nível do pool elástico.|
|/servers/elasticPools/advisors/recommendedActions/read|Retorna a lista de ações recomendadas do Supervisor especificado do pool Elástico Olá|
|/servers/elasticPools/advisors/recommendedActions/write|Aplicar Olá ação no pool Elástico Olá recomendada|
|/servers/elasticPools/elasticPoolActivity/read|Recuperar atividades e detalhes em um pool de banco de dados elástico|
|/servers/elasticPools/databases/read|Recuperar a lista e os detalhes de bancos de dados que fazem parte do pool de banco de dados elástico em determinado servidor|
|/servers/auditingPolicies/read|Recuperar detalhes da tabela de servidor padrão de saudação configurada em um determinado servidor de política de auditoria|
|/servers/auditingPolicies/write|Altera a tabela de servidor padrão de saudação auditoria para um determinado servidor|
|/servers/disasterRecoveryConfiguration/operationResults/read|Obter resultados de operação de configuração da recuperação de desastre|
|/servers/advisors/read|Retorna a lista de supervisores disponíveis para o servidor de saudação|
|/servers/advisors/write|Atualizar status de execução automática de um assistente no nível do servidor.|
|/servers/advisors/recommendedActions/read|Retorna a lista de ações recomendadas do advisor especificado para o servidor de saudação|
|/servers/advisors/recommendedActions/write|Aplicar Olá ação no servidor de saudação recomendada|
|/servers/usages/read|Cota de DTU de retorno de servidor e consuption atual de DTU por todos os bancos de dados no servidor de saudação|
|/servers/elasticPoolEstimates/read|Retornar a lista de estimativas de pool elástico já criado para o servidor|
|/servers/elasticPoolEstimates/write|Criar nova estimativa de pool elástico para a lista de bancos de dados fornecida|
|/servers/auditingSettings/read|Recuperar detalhes do blob de servidor de saudação configurada em um determinado servidor de política de auditoria|
|/servers/auditingSettings/write|Auditoria de alteração Olá servidor blob para um determinado servidor|
|/servers/auditingSettings/operationResults/read|Recuperar o resultado de blob do servidor de saudação operação de definição de política de auditoria|
|/servers/backupLongTermRetentionVaults/read|Esta operação é usada tooget um cofre de retenção de backup de longo prazo. Retorna informações sobre o servidor do hello cofre toothis registrado.|
|/servers/backupLongTermRetentionVaults/write|Registrar um cofre de retenção de backup de longo prazo|
|/servers/restorableDroppedDatabases/read|Recuperar uma lista de bancos de dados que foram descartados em determinado servidor ainda na política de retenção. Essa operação retorna uma lista de bancos de dados e metadados associados, como a data de exclusão.|
|/servers/databases/read|Retornar uma lista de servidores em um grupo de recursos de uma assinatura|
|/servers/databases/write|Criar um novo servidor ou modificar propriedades de servidor existente em um grupo de recursos de uma assinatura|
|/servers/databases/delete|Excluir um servidor e todos os bancos de dados e pools elásticos contidos|
|/servers/databases/export/action|Criar um novo banco de dados no servidor de saudação e implantar o esquema e os dados de um pacote de DacPac|
|/servers/databases/VulnerabilityAssessmentScans/action|Executar verificação de banco de dados para avaliação de vulnerabilidade.|
|/servers/databases/pause/action|Pausar um banco de dados de edição do DataWarehouse|
|/servers/databases/resume/action|Retomar um banco de dados de edição do DataWarehouse|
|/servers/databases/operationResults/read|Operação é usada tootrack andamento da operação de banco de dados em tempo de execução, como a escala.|
|/servers/databases/replicationLinks/read|Retornar detalhes sobre links de replicação estabelecidos para determinado banco de dados|
|/servers/databases/replicationLinks/delete|Encerrar a relação de replicação de saudação forçada e com potencial perda de dados|
|/servers/databases/replicationLinks/unlink/action|Encerrar a relação de replicação de saudação forçada ou após a sincronização com o parceiro Olá|
|/servers/databases/replicationLinks/failover/action|Failover após a sincronização de todas as alterações do hello primária, tornando esse banco de dados no principal de remoto da relação de replicação Olá Olá primários e fazer em um secundário|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/action|Failover imediatamente com potencial perda de dados, tornando esse banco de dados em remoto de saudação primários e fazer da relação de replicação Olá primário para um secundário|
|/servers/databases/replicationLinks/updateReplicationMode/action|Atualizar o modo de replicação para o link toosynchronous ou assíncrona|
|/servers/databases/replicationLinks/operationResults/read|Obter status de operações de longa duração em links de replicação de banco de dados|
|/servers/databases/dataMaskingPolicies/read|Recuperar os detalhes dos dados de saudação configurada em um determinado banco de dados de política de mascaramento|
|/servers/databases/dataMaskingPolicies/write|Alterar política de mascaramento de dados para determinado banco de dados|
|/servers/databases/dataMaskingPolicies/rules/read|Recuperar os detalhes dos dados de saudação configurada em um determinado banco de dados de regra de política de mascaramento|
|/servers/databases/dataMaskingPolicies/rules/write|Alterar regra de política de mascaramento de dados para determinado banco de dados|
|/servers/databases/securityAlertPolicies/read|Recuperar detalhes da política de detecção de ameaças Olá configurado em um determinado banco de dados|
|/servers/databases/securityAlertPolicies/write|Alterar a política de detecção de ameaças Olá para um determinado banco de dados|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions/read|Retornar tipos de métricas que estão disponíveis para bancos de dados|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtém a configuração de diagnóstico de saudação para o recurso de saudação|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/write|Cria ou atualiza a configuração de diagnóstico de saudação para o recurso de saudação|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions/read|Obtém os logs disponíveis Olá para bancos de dados|
|/servers/databases/topQueries/read|Retorna estatísticas de tempo de execução agregadas para a consulta selecionada no período de tempo selecionado|
|/servers/databases/topQueries/queryText/read|Retorna o texto do Transact-SQL de saudação para ID de consulta selecionada|
|/servers/databases/topQueries/statistics/read|Retorna estatísticas de tempo de execução agregadas para a consulta selecionada no período de tempo selecionado|
|/servers/databases/connectionPolicies/read|Recuperar detalhes da política de conexão de saudação configurado em um determinado banco de dados|
|/servers/databases/connectionPolicies/write|Alterar política de conexão para determinado banco de dados|
|/servers/databases/metrics/read|Retornar métrica de utilização de recursos do banco de dados|
|/servers/databases/auditRecords/read|Recuperar Olá os registros de auditoria do banco de dados blob|
|/servers/databases/transparentDataEncryption/read|Recuperar o status e os detalhes do recurso de segurança Transparent Data Encryption para determinado banco de dados|
|/servers/databases/transparentDataEncryption/write|Habilitar ou desabilitar o Transparent Data Encryption para determinado banco de dados|
|/servers/databases/transparentDataEncryption/operationResults/read|Recuperar o status e os detalhes do recurso de segurança Transparent Data Encryption para determinado banco de dados|
|/servers/databases/auditingPolicies/read|Recuperar detalhes da política de auditoria de tabela do hello configurado em um determinado banco de dados|
|/servers/databases/auditingPolicies/write|Alterar a política de auditoria de tabela Olá para um determinado banco de dados|
|/servers/databases/dataWarehouseQueries/read|Retorna informações de consulta de distribuição do hello data warehouse para a ID de consulta selecionada|
|/servers/databases/dataWarehouseQueries/<br>dataWarehouseQuerySteps/read|Olá retorna distribuídas informações de etapas de consulta da consulta de depósito de dados para a ID de etapa selecionada|
|/servers/databases/serviceTierAdvisors/read|Retornar sugestões sobre como dimensionar o banco de dados para cima ou para baixo com base no desempenho de tooimprove de estatísticas de execução de consulta ou reduzir o custo|
|/servers/databases/advisors/read|Retorna a lista de supervisores disponíveis para o banco de dados de saudação|
|/servers/databases/advisors/write|Atualizar status de um assistente no nível do banco de dados.|
|/servers/databases/advisors/recommendedActions/read|Retorna a lista de ações recomendadas do Supervisor especificado do banco de dados de saudação|
|/servers/databases/advisors/recommendedActions/write|Aplicar Olá ação no banco de dados de saudação recomendada|
|/servers/databases/usages/read|Retornar o tamanho máximo do banco de dados que pode ser alcançado e o tamanho atual ocupado por dados|
|/servers/databases/queryStore/read|Retorna os valores atuais de configurações do repositório de consultas do banco de dados de saudação|
|/servers/databases/queryStore/write|Atualiza a configuração do repositório de consultas do banco de dados de saudação|
|/servers/databases/auditingSettings/read|Recuperar detalhes da política de auditoria de blob do hello configurado em um determinado banco de dados|
|/servers/databases/auditingSettings/write|Alterar a política de auditoria de blob Olá para um determinado banco de dados|
|/servers/databases/schemas/tables/recommendedIndexes/read|Recuperar a lista de recomendações de índice em um banco de dados|
|/servers/databases/schemas/tables/recommendedIndexes/write|Aplicar a recomendação de índice|
|/servers/databases/schemas/tables/columns/read|Recuperar a lista de colunas de uma tabela|
|/servers/databases/missingindexes/read|Retornar sugestões sobre toocreate de índices do banco de dados, modificar ou Excluir ordem tooimprove desempenho de consulta|
|/servers/databases/missingindexes/write|Usar recomendação de índice de banco de dados em determinado banco de dados|
|/servers/databases/importExportOperationResults/read|Retornar detalhes sobre a operação de importação ou exportação de banco de dados de DacPac localizado na conta de armazenamento|
|/servers/importExportOperationResults/read|Retornar a lista de saudação com detalhes para operações de importação de banco de dados da conta de armazenamento em um determinado servidor|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Operação | Descrição |
|---|---|
|/register/action|Registra a assinatura Olá para o provedor de recursos de armazenamento hello e permite a criação de saudação de contas de armazenamento.|
|/checknameavailability/read|Verificar se o nome dessa conta é válido e não está em uso.|
|/storageAccounts/write|Cria uma conta de armazenamento com hello especificado parâmetros ou atualização Olá propriedades ou marcas ou adiciona personalizado domínio Olá especificou a conta de armazenamento.|
|/storageAccounts/delete|Excluir uma conta de armazenamento existente.|
|/storageAccounts/listkeys/action|Retorna Olá chaves de acesso para hello especificou a conta de armazenamento.|
|/storageAccounts/regeneratekey/action|Regenera Olá chaves de acesso para Olá especificado a conta de armazenamento.|
|/storageAccounts/read|Olá retorna a lista de contas de armazenamento ou obtém Olá propriedades Olá especificadas conta de armazenamento.|
|/storageAccounts/listAccountSas/action|Token de SAS da conta de saudação retorna para Olá especificado a conta de armazenamento.|
|/storageAccounts/listServiceSas/action|Token SAS do serviço de armazenamento|
|/storageAccounts/services/diagnosticSettings/write|Criar/atualizar definições de diagnóstico da conta de armazenamento.|
|/skus/read|Lista Olá Skus com o suporte da Microsoft.|
|/usages/read|Retorna Olá limite e contagem de uso atual Olá para recursos Olá especificado assinatura|
|/operations/read|Pesquisas Olá status de uma operação assíncrona.|
|/locations/deleteVirtualNetworkOrSubnets/action|Notificar o Microsoft.Storage sobre a exclusão de uma rede virtual ou sub-rede|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Operação | Descrição |
|---|---|
|/managers/clearAlerts/action|Limpe todos os alertas de saudação associados ao Gerenciador de dispositivo de saudação.|
|/managers/getActivationKey/action|Obter chave de ativação para o Gerenciador de dispositivos hello.|
|/managers/regenerateActivationKey/action|Regenerar a chave de ativação para o Gerenciador de dispositivos hello.|
|/managers/regenarateRegistationCertificate/action|Regenerar o registro de certificado para gerenciadores de saudação do dispositivo.|
|/managers/getEncryptionKey/action|Obter chave de criptografia para o Gerenciador de dispositivos hello.|
|/managers/read|Lista ou obtém gerenciadores de saudação do dispositivo|
|/managers/delete|Exclui os gerenciadores de saudação do dispositivo|
|/managers/write|Criar ou atualizar gerenciadores de saudação do dispositivo|
|/managers/configureDevice/action|Configurar um dispositivo|
|/managers/listActivationKey/action|Obtém a chave de ativação de saudação do hello Gerenciador de dispositivos do StorSimple.|
|/managers/listPublicEncryptionKey/action|Listar chaves de criptografia públicas de um Gerenciador de Dispositivo StorSimple.|
|/managers/listPrivateEncryptionKey/action|Obter a chave de criptografia particular para um Gerenciador de Dispositivos StorSimple.|
|/managers/provisionCloudAppliance/action|Criar um novo dispositivo de nuvem.|
|/Managers/write|A operação Criar cofre cria um recurso do Azure do tipo 'cofre'|
|/Managers/read|Olá operação obter cofre obtém um objeto que representa a saudação recursos do Azure do tipo 'cofre'|
|/Managers/delete|Olá Olá de exclusões de operação Excluir cofre especificado recursos do Azure do tipo 'cofre'|
|/managers/storageAccountCredentials/write|Criar ou atualizar as credenciais de conta de armazenamento Olá|
|/managers/storageAccountCredentials/read|Lista ou obtém Olá credenciais da conta de armazenamento|
|/managers/storageAccountCredentials/delete|Exclui as credenciais de conta de armazenamento Olá|
|/managers/storageAccountCredentials/listAccessKey/action|Listar chaves de acesso de credenciais da conta de armazenamento|
|/managers/accessControlRecords/read|Lista ou obtém Olá registros de controle de acesso|
|/managers/accessControlRecords/write|Criar ou atualizar registros de controle de acesso de saudação|
|/managers/accessControlRecords/delete|Exclui registros de controle de acesso de saudação|
|/managers/metrics/read|Lista ou obtém Olá métricas|
|/managers/bandwidthSettings/read|Lista as configurações de largura de banda de saudação (8000 Series apenas)|
|/managers/bandwidthSettings/write|Criar novas configurações de largura de banda ou atualizá-las (somente 8000 Series)|
|/managers/bandwidthSettings/delete|Excluir uma configuração de largura de banda existente (somente 8000 Series)|
|/Managers/extendedInformation/read|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/Managers/extendedInformation/write|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/Managers/extendedInformation/delete|Olá operação obter informações estendidas obtém informações estendidas de um objeto que representa a saudação tipo de recurso do Azure? cofre?|
|/managers/alerts/read|Lista ou obtém Olá alertas|
|/managers/storageDomains/read|Lista ou obtém Olá domínios de armazenamento|
|/managers/storageDomains/write|Criar ou atualizar domínios de armazenamento Olá|
|/managers/storageDomains/delete|Exclui Olá domínios de armazenamento|
|/managers/devices/scanForUpdates/action|Verificar se há atualizações em um dispositivo.|
|/managers/devices/download/action|Baixar atualizações para um dispositivo.|
|/managers/devices/install/action|Instalar atualizações em um dispositivo.|
|/managers/devices/read|Lista ou obtém Olá dispositivos|
|/managers/devices/write|Criar ou atualizar dispositivos Olá|
|/managers/devices/delete|Exclui Olá dispositivos|
|/managers/devices/deactivate/action|Desativar um dispositivo.|
|/managers/devices/publishSupportPackage/action|Publicar o pacote de suporte de um dispositivo para solução de problemas pelo Suporte da Microsoft.|
|/managers/devices/failover/action|Failover de dispositivo de saudação.|
|/managers/devices/sendTestAlertEmail/action|Envie email de alerta de teste tooconfigured destinatários de email.|
|/managers/devices/installUpdates/action|Instala as atualizações nos dispositivos Olá|
|/managers/devices/listFailoverSets/action|Define a lista Olá failover para um dispositivo existente.|
|/managers/devices/listFailoverTargets/action|Lista de destinos de failover de dispositivos de saudação|
|/managers/devices/publicEncryptionKey/action|Chave de criptografia pública de lista do Gerenciador de dispositivos Olá|
|/managers/devices/hardwareComponentGroups/<br>leitura|Olá lista grupos de componentes de Hardware|
|/managers/devices/hardwareComponentGroups/<br>changeControllerPowerState/action|Alterar o estado de energia do controlador dos grupos de componentes de hardware|
|/managers/devices/metrics/read|Lista ou obtém Olá métricas|
|/managers/devices/chapSettings/write|Criar ou atualizar as configurações de Chap Olá|
|/managers/devices/chapSettings/read|Lista ou obtém as configurações de Chap Olá|
|/managers/devices/chapSettings/delete|Exclui as configurações de Chap Olá|
|/managers/devices/backupScheduleGroups/read|Lista ou obtém Olá grupos de agendamento de Backup|
|/managers/devices/backupScheduleGroups/write|Criar ou atualizar grupos de agendamento de Backup Olá|
|/managers/devices/backupScheduleGroups/delete|Exclui Olá grupos de agendamento de Backup|
|/managers/devices/updateSummary/read|Lista ou obtém Olá Resumo da atualização|
|/managers/devices/migrationSourceConfigurations/<br>import/action|Importar configurações de origem para migração|
|/managers/devices/migrationSourceConfigurations/<br>startMigrationEstimate/action|Inicie um trabalho tooestimate Olá durante saudação processo de migração.|
|/managers/devices/migrationSourceConfigurations/<br>startMigration/action|Iniciar migração usando as configurações de origem|
|/managers/devices/migrationSourceConfigurations/<br>confirmMigration/action|Confirmar uma migração bem-sucedida.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationEstimate/action|Busca o status de saudação para o trabalho de estimativa de migração de saudação.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationStatus/action|Busca o status de saudação para migração de saudação.|
|/managers/devices/migrationSourceConfigurations/<br>fetchConfirmMigrationStatus/action|Saudação de busca confirmar o status de migração.|
|/managers/devices/alertSettings/read|Lista ou obtém as configurações de alerta de saudação|
|/managers/devices/alertSettings/write|Criar ou atualizar as configurações de alerta de saudação|
|/managers/devices/networkSettings/read|Lista ou obtém as configurações de rede Olá|
|/managers/devices/networkSettings/write|Criar novas ou atualizar as configurações de rede|
|/managers/devices/jobs/read|Lista ou obtém trabalhos Olá|
|/managers/devices/jobs/cancel/action|Cancelar um trabalho em execução|
|/managers/devices/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/devices/volumeContainers/write|Criar novos ou atualizar os contêineres de volume (somente 8000 Series)|
|/managers/devices/volumeContainers/read|Lista de contêineres de Volume hello (8000 Series apenas)|
|/managers/devices/volumeContainers/delete|Excluir contêineres de Volume existentes (somente 8000 Series)|
|/managers/devices/volumeContainers/listEncryptionKeys/action|Listar chaves de criptografia da lista de contêineres de volume|
|/managers/devices/volumeContainers/rolloverEncryptionKey/action|Chaves de criptografia de substituição de contêineres de volume|
|/managers/devices/volumeContainers/metrics/read|Lista as métricas de saudação|
|/managers/devices/volumeContainers/volumes/read|Olá lista Volumes|
|/managers/devices/volumeContainers/volumes/write|Criar ou atualizar volumes|
|/managers/devices/volumeContainers/volumes/delete|Excluir um volume existente|
|/managers/devices/volumeContainers/volumes/metrics/read|Lista as métricas de saudação|
|/managers/devices/volumeContainers/volumes/metricsDefinitions/read|Olá lista definições de métricas|
|/managers/devices/volumeContainers/metricsDefinitions/read|Olá lista definições de métricas|
|/managers/devices/iscsiservers/read|Lista ou obtém Olá iSCSI servidores|
|/managers/devices/iscsiservers/write|Criar ou atualizar Olá iSCSI servidores|
|/managers/devices/iscsiservers/delete|Exclui Olá iSCSI servidores|
|/managers/devices/iscsiservers/backup/action|Fazer backup de um servidor iSCSI.|
|/managers/devices/iscsiservers/metrics/read|Lista ou obtém Olá métricas|
|/managers/devices/iscsiservers/disks/read|Lista ou obtém Olá discos|
|/managers/devices/iscsiservers/disks/write|Criar ou atualizar Olá discos|
|/managers/devices/iscsiservers/disks/delete|Exclui Olá discos|
|/managers/devices/iscsiservers/disks/metrics/read|Lista ou obtém Olá métricas|
|/managers/devices/iscsiservers/disks/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/devices/iscsiservers/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/devices/backups/read|Lista ou obtém saudação do conjunto de Backup|
|/managers/devices/backups/delete|Exclusões Olá do conjunto de Backup|
|/managers/devices/backups/restore/action|Restaure todos os volumes de saudação de um conjunto de backup.|
|/managers/devices/backups/elements/clone/action|Clonar um compartilhamento ou volume usando um elemento de backup.|
|/managers/devices/backupPolicies/write|Criar novas ou atualizar as políticas de Backup (somente 8000 Series)|
|/managers/devices/backupPolicies/read|Olá lista as políticas de Backup (8000 Series apenas)|
|/managers/devices/backupPolicies/delete|Excluir políticas de backup existentes (somente 8000 Series)|
|/managers/devices/backupPolicies/backup/action|Um toocreate backup manual uma demanda fazer backup de todos os volumes de saudação protegidos pela política de saudação.|
|/managers/devices/backupPolicies/schedules/write|Criar ou atualizar agendas|
|/managers/devices/backupPolicies/schedules/read|Lista Olá agendas|
|/managers/devices/backupPolicies/schedules/delete|Excluir agendas existentes|
|/managers/devices/securitySettings/update/action|Atualize as configurações de segurança de saudação.|
|/managers/devices/securitySettings/read|Olá lista as configurações de segurança|
|/managers/devices/securitySettings/<br>syncRemoteManagementCertificate/action|Sincronize o certificado de gerenciamento remoto de saudação para um dispositivo.|
|/managers/devices/securitySettings/write|Criar ou atualizar as configurações de segurança|
|/managers/devices/fileservers/read|Lista ou obtém servidores de arquivo hello|
|/managers/devices/fileservers/write|Criar ou atualizar os servidores de arquivos Olá|
|/managers/devices/fileservers/delete|Exclui Olá servidores de arquivos|
|/managers/devices/fileservers/backup/action|Fazer backup de um servidor de arquivos.|
|/managers/devices/fileservers/metrics/read|Lista ou obtém Olá métricas|
|/managers/devices/fileservers/shares/write|Criar ou atualizar compartilhamentos Olá|
|/managers/devices/fileservers/shares/read|Lista ou obtém Olá compartilhamentos|
|/managers/devices/fileservers/shares/delete|Exclui Olá compartilhamentos|
|/managers/devices/fileservers/shares/metrics/read|Lista ou obtém Olá métricas|
|/managers/devices/fileservers/shares/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/devices/fileservers/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/devices/timeSettings/read|Lista ou obtém as configurações de tempo de saudação|
|/managers/devices/timeSettings/write|Criar ou atualizar as configurações de tempo|
|/Managers/certificates/write|Olá a operação de certificado do recurso de atualização atualiza o certificado de credencial de cofre/recurso hello.|
|/managers/cloudApplianceConfigurations/read|Olá lista configurações de suporte de dispositivos de nuvem|
|/managers/metricsDefinitions/read|Lista ou obtém as definições de métricas de saudação|
|/managers/encryptionSettings/read|Lista ou obtém as configurações de criptografia de saudação|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Operação | Descrição |
|---|---|
|/streamingjobs/Start/action|Iniciar trabalho do Stream Analytics|
|/streamingjobs/Stop/action|Interromper trabalho do Stream Analytics|
|/streamingjobs/Read|Ler trabalho do Stream Analytics|
|/streamingjobs/Write|Gravar trabalho de Stream Analytics|
|/streamingjobs/Delete|Excluir trabalho de Stream Analytics|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/read|Obtém métricas disponíveis Olá para streamingjobs|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/read|Ler configuração de diagnóstico.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/write|Gravar configuração de diagnóstico.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/read|Obtém os logs disponíveis Olá para streamingjobs|
|/streamingjobs/transformations/Read|Ler transformação do trabalho do Stream Analytics|
|/streamingjobs/transformations/Write|Gravar transformação do trabalho do Stream Analytics|
|/streamingjobs/transformations/Delete|Excluir transformação do trabalho do Stream Analytics|
|/streamingjobs/inputs/Read|Ler entrada do trabalho do Stream Analytics|
|/streamingjobs/inputs/Write|Gravar entrada de trabalho do Stream Analytics|
|/streamingjobs/inputs/Delete|Excluir entrada de trabalho do Stream Analytics|
|/streamingjobs/outputs/Read|Ler saída do trabalho do Stream Analytics|
|/streamingjobs/outputs/Write|Gravar saída de trabalho do Stream Analytics|
|/streamingjobs/outputs/Delete|Excluir saída de trabalho do Stream Analytics|

## <a name="microsoftsupport"></a>Microsoft.Support

| Operação | Descrição |
|---|---|
|/register/action|Registra o provedor de recursos de tooSupport|
|/supportTickets/read|Obtém detalhes de tíquete de suporte (incluindo status, gravidade, detalhes de contato e comunicações) ou obtém a lista de saudação de tíquetes de suporte entre assinaturas.|
|/supportTickets/write|Criar ou atualizar um tíquete de suporte. Você pode criar um tíquete de suporte para problemas técnicos, de cotas, de cobrança ou de gerenciamento de assinaturas. Você pode atualizar severidade, detalhes de contato e comunicações de tíquetes de suporte existentes.|

## <a name="microsoftweb"></a>Microsoft.Web

| Operação | Descrição |
|---|---|
|/unregister/action|Cancelar o registro do provedor de recursos do Microsoft para assinatura de saudação.|
|/validate/action|Validar.|
|/register/action|Registre o provedor de recursos do Microsoft para assinatura de saudação.|
|/hostingEnvironments/Read|Obter propriedades de saudação de um ambiente de serviço de aplicativo|
|/hostingEnvironments/Write|Criar um novo Ambiente do Serviço de Aplicativo ou atualizar um existente|
|/hostingEnvironments/Delete|Excluir ambiente do Serviço de Aplicativo|
|/hostingEnvironments/reboot/Action|Reinicializar todas as máquinas em um Ambiente do Serviço de Aplicativo|
|/hostingenvironments/resume/action|Retomar ambientes de hospedagem.|
|/hostingenvironments/suspend/action|Suspender ambientes de hospedagem.|
|/hostingenvironments/metricdefinitions/read|Obter definições de métrica de ambientes de hospedagem.|
|/hostingEnvironments/workerPools/Read|Obter propriedades de saudação de um Pool de trabalho em um ambiente de serviço de aplicativo|
|/hostingEnvironments/workerPools/Write|Criar um novo pool de trabalho em um Ambiente do Serviço de Aplicativo ou atualizar um existente|
|/hostingenvironments/workerpools/metricdefinitions/read|Obter definições de métrica de pools de trabalho dos ambientes de hospedagem.|
|/hostingenvironments/workerpools/metrics/read|Obter a métrica de pools de trabalho de Ambientes de Hospedagem.|
|/hostingenvironments/workerpools/skus/read|Obter SKUs de pools de trabalho dos ambientes de hospedagem.|
|/hostingenvironments/workerpools/usages/read|Obter uso dos pools de trabalho dos ambientes de hospedagem.|
|/hostingenvironments/sites/read|Obter aplicativos Web dos ambientes de hospedagem.|
|/hostingenvironments/serverfarms/read|Obter Planos do Serviço de Aplicativo dos Ambientes de Hospedagem.|
|/hostingenvironments/usages/read|Obter usos dos ambientes de hospedagem.|
|/hostingenvironments/capacities/read|Obter as capacidades dos ambientes de hospedagem.|
|/hostingenvironments/operations/read|Obter operações dos ambientes de hospedagem.|
|/hostingEnvironments/multiRolePools/Read|Obter propriedades de saudação de um Pool de front-end em um ambiente de serviço de aplicativo|
|/hostingEnvironments/multiRolePools/Write|Criar um novo pool de front-end em um Ambiente do Serviço de Aplicativo ou atualizar um existente|
|/hostingenvironments/multirolepools/metricdefinitions/read|Obter definições de métrica de pools multifunção dos ambientes de hospedagem.|
|/hostingenvironments/multirolepools/metrics/read|Obter a métrica de pools multifunção em Ambientes de Hospedagem.|
|/hostingenvironments/multirolepools/skus/read|Obter SKUs de pools multifunção dos ambientes de hospedagem.|
|/hostingenvironments/multirolepools/usages/read|Obter usos dos pools multifunção dos ambientes de hospedagem.|
|/hostingenvironments/diagnostics/read|Obter diagnóstico dos ambientes de hospedagem.|
|/publishingusers/read|Obter usuários de publicação.|
|/publishingusers/write|Atualizar usuários de publicação.|
|/checknameavailability/read|Verificar se o nome do recurso está disponível.|
|/geoRegions/Read|Obter lista de saudação das regiões geográfica.|
|/sites/Read|Obter propriedades de saudação de um aplicativo Web|
|/sites/Write|Criar um novo aplicativo Web ou atualizar um existente|
|/sites/Delete|Excluir um aplicativo Web existente|
|/sites/backup/Action|Criar um novo backup do aplicativo Web|
|/sites/publishxml/Action|Obter XML do perfil de publicação para um aplicativo Web|
|/sites/publish/Action|Publicar um aplicativo Web|
|/sites/restart/Action|Reiniciar um aplicativo Web|
|/sites/start/Action|Iniciar um aplicativo Web|
|/sites/stop/Action|Interromper um aplicativo Web|
|/sites/slotsswap/Action|Trocar slots de implantação de aplicativo Web|
|/sites/slotsdiffs/Action|Obter as diferenças de configuração entre aplicativo web e slots|
|/sites/applySlotConfig/Action|Aplicar a configuração do slot de aplicativo web do aplicativo de web atual do destino slot toohello|
|/sites/resetSlotConfig/Action|Redefinir a configuração de aplicativo Web|
|/sites/functions/action|Aplicativos Web do Functions.|
|/sites/listsyncfunctiontriggerstatus/action|Listar Aplicativos Web de status do gatilho da função de sincronização.|
|/sites/networktrace/action|Aplicativos Web de rastreamento de rede.|
|/sites/newpassword/action|Aplicativos Web Newpassword.|
|/sites/sync/action|Sincronizar pplicativos Web.|
|/sites/operationresults/read|Obter resultados de operação de aplicativos Web.|
|/sites/webjobs/read|Obter trabalhos da Web de aplicativos Web.|
|/sites/backup/read|Obter o backup de aplicativos Web.|
|/sites/backup/write|Atualizar o backup de aplicativos Web.|
|/sites/metricdefinitions/read|Obter definições de métrica de aplicativos Web.|
|/sites/metrics/read|Métrica de aplicativos Web.|
|/sites/continuouswebjobs/delete|Excluir trabalhos da Web contínuos de aplicativos Web.|
|/sites/continuouswebjobs/read|Obter trabalhos de Web contínuos de aplicativos Web.|
|/sites/continuouswebjobs/start/action|Iniciar trabalhos de Web contínuos de aplicativos Web.|
|/sites/continuouswebjobs/stop/action|Interromper trabalhos de Web contínuos de aplicativos Web.|
|/sites/domainownershipidentifiers/read|Obter identificadores de propriedade de domínio de aplicativos Web.|
|/sites/domainownershipidentifiers/write|Atualizar de identificadores de propriedade de domínio de aplicativos Web.|
|/sites/premieraddons/delete|Excluir complementos Premier de aplicativos Web.|
|/sites/premieraddons/read|Obter complementos Premier de aplicativos Web.|
|/sites/premieraddons/write|Atualizar complementos Premier de aplicativos Web.|
|/sites/triggeredwebjobs/delete|Excluir trabalhos da Web disparados para aplicativos Web.|
|/sites/triggeredwebjobs/read|Obter trabalhos da Web disparados de aplicativos Web.|
|/sites/triggeredwebjobs/run/action|Executar trabalhos da Web disparados de aplicativos Web.|
|/sites/hostnamebindings/delete|Excluir associações de nome de host de aplicativos Web.|
|/sites/hostnamebindings/read|Obter associações de nome de host de aplicativos Web.|
|/sites/hostnamebindings/write|Atualizar associações de nome de host de aplicativos Web.|
|/sites/virtualnetworkconnections/delete|Excluir as conexões de rede virtual de aplicativos Web.|
|/sites/virtualnetworkconnections/read|Obter as conexões de rede virtual de aplicativos Web.|
|/sites/virtualnetworkconnections/write|Atualizar as conexões de rede virtual de aplicativos Web.|
|/sites/virtualnetworkconnections/gateways/read|Obter gateways de conexões de rede virtual de aplicativos Web.|
|/sites/virtualnetworkconnections/gateways/write|Atualizar gateways de conexões de rede virtual de aplicativos Web.|
|/sites/publishxml/read|Obter XML de publicação de aplicativos Web.|
|/sites/hybridconnectionrelays/read|Obter transmissões de conexão híbrida de aplicativos Web.|
|/sites/perfcounters/read|Obter contadores de desempenho de aplicativos Web.|
|/sites/usages/read|Obter usos de aplicativos Web.|
|/sites/slots/Write|Criar um novo slot do aplicativo Web ou atualizar um existente|
|/sites/slots/Delete|Excluir um slot de aplicativo Web existente|
|/sites/slots/backup/Action|Criar o novo backup do slot do aplicativo Web.|
|/sites/slots/publishxml/Action|Obter XML do perfil de publicação para um slot de aplicativo Web|
|/sites/slots/publish/Action|Publicar um slot do aplicativo Web|
|/sites/slots/restart/Action|Reiniciar um slot de aplicativo Web|
|/sites/slots/start/Action|Iniciar um slot de aplicativo Web|
|/sites/slots/stop/Action|Interromper um slot de aplicativo Web|
|/sites/slots/slotsswap/Action|Trocar slots de implantação de aplicativo Web|
|/sites/slots/slotsdiffs/Action|Obter as diferenças de configuração entre aplicativo web e slots|
|/sites/slots/applySlotConfig/Action|Aplica a configuração do slot de aplicativo web do slot atual de toohello de slot de destino.|
|/sites/slots/resetSlotConfig/Action|Redefinir a configuração de slot do aplicativo Web|
|/sites/slots/Read|Obter propriedades de saudação de um slot de implantação de aplicativo Web|
|/sites/slots/newpassword/action|Slots de aplicativos Web Newpassword.|
|/sites/slots/sync/action|Sincronizar slots de aplicativos Web.|
|/sites/slots/operationresults/read|Obter resultados de operação de slots de aplicativos Web.|
|/sites/slots/webjobs/read|Obter trabalhos da Web dos slots de aplicativos Web.|
|/sites/slots/backup/write|Atualizar o backup de slots de aplicativos Web.|
|/sites/slots/metricdefinitions/read|Obter definições de métrica de slots de aplicativos Web.|
|/sites/slots/metrics/read|Obter métrica dos slots de aplicativos Web.|
|/sites/slots/continuouswebjobs/delete|Excluir trabalhos da Web contínuos de slots de aplicativos Web.|
|/sites/slots/continuouswebjobs/read|Obter trabalhos da Web contínuos de slots de aplicativos Web.|
|/sites/slots/continuouswebjobs/start/action|Iniciar trabalhos da Web contínuos de slots de aplicativos Web.|
|/sites/slots/continuouswebjobs/stop/action|Interromper trabalhos da Web contínuos de slots de aplicativos Web.|
|/sites/slots/premieraddons/delete|Excluir complementos de Premier de slots de aplicativos Web.|
|/sites/slots/premieraddons/read|Obter complementos Premier de slots de aplicativos Web.|
|/sites/slots/premieraddons/write|Atualizar complementos Premier de slots de aplicativos Web.|
|/sites/slots/triggeredwebjobs/delete|Excluir trabalhos da Web disparados de slots de aplicativos Web.|
|/sites/slots/triggeredwebjobs/read|Obter trabalhos da Web disparados de slots de aplicativos Web.|
|/sites/slots/triggeredwebjobs/run/action|Executar trabalhos da Web dos slots de aplicativos Web.|
|/sites/slots/hostnamebindings/delete|Excluir vínculos de nome de host de slots de aplicativos Web.|
|/sites/slots/hostnamebindings/read|Obter vínculos de nome de host de slots de aplicativos Web.|
|/sites/slots/hostnamebindings/write|Atualizar vínculos de nome de host de slots de aplicativos Web.|
|/sites/slots/phplogging/read|Obter Phplogging dos slots de aplicativos Web.|
|/sites/slots/virtualnetworkconnections/delete|Excluir conexões de rede virtual de slots de aplicativos Web.|
|/sites/slots/virtualnetworkconnections/read|Obter conexões de rede virtual dos slots de aplicativos Web.|
|/sites/slots/virtualnetworkconnections/write|Atualizar conexões de rede virtual de slots de aplicativos Web.|
|/sites/slots/virtualnetworkconnections/gateways/write|Atualizar gateways de conexões de rede virtual de slots de aplicativos Web.|
|/sites/slots/usages/read|Obter usos dos slots de aplicativos Web.|
|/sites/slots/hybridconnection/delete|Excluir a conexão híbrida de slots de aplicativos Web.|
|/sites/slots/hybridconnection/read|Obter a conexão híbrida de slots de aplicativos Web.|
|/sites/slots/hybridconnection/write|Atualizar a conexão híbrida de slots de aplicativos Web.|
|/sites/slots/config/Read|Obter definições de configuração do slot do aplicativo Web|
|/sites/slots/config/list/Action|Listar as configurações confidenciais de segurança do slot do aplicativo Web, como credenciais de publicação, configurações do aplicativo e cadeias de conexão|
|/sites/slots/config/Write|Atualizar definições de configuração do slot do aplicativo Web|
|/sites/slots/config/delete|Excluir configuração de slots de aplicativos Web.|
|/sites/slots/instances/read|Obter instâncias dos slots de aplicativos Web.|
|/sites/slots/instances/processes/read|Obter os processos de instâncias dos slots de aplicativos Web.|
|/sites/slots/instances/deployments/read|Obter as implantações de instâncias dos slots de aplicativos Web.|
|/sites/slots/sourcecontrols/Read|Obter definições de configuração de controle de origem do slot do aplicativo Web|
|/sites/slots/sourcecontrols/Write|Atualizar definições de configuração de controle de origem do slot do aplicativo Web|
|/sites/slots/sourcecontrols/Delete|Excluir definições de configuração de controle de origem do slot do aplicativo Web|
|/sites/slots/restore/read|Obter a restauração dos slots de aplicativos Web.|
|/sites/slots/analyzecustomhostname/read|Obter slots de aplicativos Web Analisar nome de host personalizado.|
|/sites/slots/backups/Read|Obter propriedades de saudação do backup dos slots um aplicativo web|
|/sites/slots/backups/list/action|Listar backups de slots de aplicativos de Web.|
|/sites/slots/backups/restore/action|Restaurar backups de slots de aplicativos Web.|
|/sites/slots/deployments/delete|Excluir as implantações de slots de aplicativos Web.|
|/sites/slots/deployments/read|Obter as implantações dos slots de aplicativos Web.|
|/sites/slots/deployments/write|Atualizar as implantações de slots de aplicativos Web.|
|/sites/slots/deployments/log/read|Obter o log de implantações dos slots de aplicativos Web.|
|/sites/hybridconnection/delete|Excluir a conexão híbrida de aplicativos Web.|
|/sites/hybridconnection/read|Obter a conexão híbrida de aplicativos Web.|
|/sites/hybridconnection/write|Atualizar a conexão híbrida de aplicativos Web.|
|/sites/recommendationhistory/read|Obter o histórico de recomendação de aplicativos Web.|
|/sites/recommendations/Read|Obter lista de saudação de recomendações para o aplicativo web.|
|/sites/recommendations/disable/action|Desabilitar as recomendações de aplicativos Web.|
|/sites/config/Read|Obter definições de configuração do aplicativo Web|
|/sites/config/list/Action|Listar as configurações confidenciais de segurança do aplicativo Web, como credenciais de publicação, configurações do aplicativo e cadeias de conexão|
|/sites/config/Write|Atualizar definições de configuração do aplicativo Web|
|/sites/config/delete|Excluir configuração de aplicativos Web.|
|/sites/instances/read|Obter instâncias de aplicativos Web.|
|/sites/instances/processes/delete|Excluir processos de instâncias de aplicativos Web.|
|/sites/instances/processes/read|Obter os processos de instâncias de aplicativos Web.|
|/sites/instances/deployments/read|Obter as implantações de instâncias de aplicativos Web.|
|/sites/sourcecontrols/Read|Obter configurações de controle de origem do aplicativo Web|
|/sites/sourcecontrols/Write|Atualizar definições de configuração de controle de origem do aplicativo Web|
|/sites/sourcecontrols/Delete|Excluir definições de configuração de controle de origem do aplicativo Web|
|/sites/restore/read|Obter a restauração de aplicativos Web.|
|/sites/analyzecustomhostname/read|Analisar nome de host personalizado.|
|/sites/backups/Read|Obter propriedades de saudação do backup de um aplicativo web|
|/sites/backups/list/action|Listar backups de aplicativos de Web.|
|/sites/backups/restore/action|Restaurar backups de aplicativos Web.|
|/sites/snapshots/read|Obter instantâneos de aplicativos Web.|
|/sites/functions/delete|Excluir funções de aplicativos Web.|
|/sites/functions/listsecrets/action|Listar segredos de funções de aplicativos Web.|
|/sites/functions/read|Obter funções de aplicativos Web.|
|/sites/functions/write|Atualizar funções de aplicativos Web.|
|/sites/deployments/delete|Excluir as implantações de aplicativos Web.|
|/sites/deployments/read|Obter as implantações de aplicativos Web.|
|/sites/deployments/write|Atualizar as implantações de aplicativos Web.|
|/sites/deployments/log/read|Obter o log de implantações de aplicativos Web.|
|/sites/diagnostics/read|Obter o diagnóstico de aplicativos Web.|
|/sites/diagnostics/workerprocessrecycle/read|Obter a reciclagem do processo de trabalho do diagnóstico de aplicativos Web.|
|/sites/diagnostics/workeravailability/read|Obter Workeravailability de diagnóstico de aplicativos Web.|
|/sites/diagnostics/runtimeavailability/read|Obter a disponibilidade de tempo de execução do diagnóstico de aplicativos Web.|
|/sites/diagnostics/cpuanalysis/read|Obter Cpuanalysis de diagnóstico de aplicativos Web.|
|/sites/diagnostics/servicehealth/read|Obter integridade do serviço de diagnóstico de aplicativos Web.|
|/sites/diagnostics/frebanalysis/read|Obter a análise FREB do diagnóstico de aplicativos Web.|
|/availablestacks/read|Obter pilhas disponíveis.|
|/isusernameavailable/read|Verificar se o nome de usuário está disponível.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Read|Obter lista de saudação de Apis.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Write|Adicionar uma nova API ou atualizar uma existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Delete|Excluir uma API existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Read|Obter lista de saudação de conexões.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Write|Salvar uma nova conexão ou atualizar uma existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Delete|Remover uma conexão existente.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Read|Ler ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Write|Adicionar ou atualizar ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Delete|Excluir ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connectionAcls/Read|Ler ConnectionAcls para a API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Read|Ler ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Write|Criar ou atualizar as ACLS de API|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Delete|Excluir ACLS de API|
|/serverfarms/Read|Obter propriedades de saudação em um plano de serviço de aplicativo|
|/serverfarms/Write|Criar um novo Plano do Serviço de Aplicativo ou atualizar um plano existente|
|/serverfarms/Delete|Excluir um Plano do Serviço de Aplicativo existente|
|/serverfarms/restartSites/Action|Reiniciar todos os aplicativos Web em um Plano do Serviço de Aplicativo|
|/serverfarms/operationresults/read|Obter resultados de operação dos Planos do Serviço de Aplicativo.|
|/serverfarms/capabilities/read|Obter recursos do Planos do Serviço de Aplicativo.|
|/serverfarms/metricdefinitions/read|Obter definições de métrica dos Planos do Serviço de Aplicativo.|
|/serverfarms/metrics/read|Obter métrica dos Planos do Serviço de Aplicativo.|
|/serverfarms/hybridconnectionplanlimits/read|Obter limites do plano de conexão híbrida dos Planos do Serviço de Aplicativo.|
|/serverfarms/virtualnetworkconnections/read|Obter as conexões de rede virtual dos Planos do Serviço de Aplicativo.|
|/serverfarms/virtualnetworkconnections/routes/delete|Excluir rotas de conexões de rede virtual dos Planos do Serviço de Aplicativo.|
|/serverfarms/virtualnetworkconnections/routes/read|Obter a rotas de conexões de rede virtual dos Planos do Serviço de Aplicativo.|
|/serverfarms/virtualnetworkconnections/routes/write|Atualizar rotas de conexões de rede virtual dos Planos do Serviço de Aplicativo.|
|/serverfarms/virtualnetworkconnections/gateways/write|Atualizar gateways de conexões de rede virtual dos Planos do Serviço de Aplicativo.|
|/serverfarms/firstpartyapps/settings/delete|Excluir configurações de aplicativos próprios dos Planos do Serviço de Aplicativo.|
|/serverfarms/firstpartyapps/settings/read|Obter configurações de aplicativos próprios dos Planos do Serviço de Aplicativo.|
|/serverfarms/firstpartyapps/settings/write|Atualizar configurações de aplicativos próprios dos Planos do Serviço de Aplicativo.|
|/serverfarms/sites/read|Obter aplicativos Web dos Planos do Serviço de Aplicativo.|
|/serverfarms/workers/reboot/action|Reinicializar trabalhos dos Planos do Serviço de Aplicativo.|
|/serverfarms/hybridconnectionrelays/read|Obter transmissões de conexão híbrida dos Planos do Serviço de Aplicativo.|
|/serverfarms/skus/read|Obter as SKUs dos Planos do Serviço de Aplicativo.|
|/serverfarms/usages/read|Obter usos dos Planos do Serviço de Aplicativo.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/read|Obter aplicativos Web das retransmissões dos namespaces da conexão híbrida dos Planos do Serviço de Aplicativo.|
|/ishostnameavailable/read|Verificar se o nome do host está disponível.|
|/connectionGateways/Read|Obter lista de saudação de Gateways de Conexão.|
|/connectionGateways/Write|Criar ou atualizar um Gateway de Conexão.|
|/connectionGateways/Delete|Excluir um Gateway de Conexão.|
|/connectionGateways/Join/Action|Adicionar um Gateway de Conexão.|
|/classicmobileservices/read|Obter Serviços Móveis clássicos.|
|/skus/read|Obter SKUs.|
|/certificates/Read|Obter lista de saudação de certificados.|
|/certificates/Write|Adicionar um novo certificado ou atualizar um existente.|
|/certificates/Delete|Excluir um certificado existente.|
|/operations/read|Obter Operações.|
|/recommendations/Read|Obter lista de saudação de recomendações para assinaturas.|
|/ishostingenvironmentnameavailable/read|Obter confirmação se o nome do ambiente de hospedagem está disponível.|
|/apiManagementAccounts/Read|Obter lista de saudação do ApiManagementAccounts.|
|/apiManagementAccounts/Write|Adicionar uma nova ApiManagementAccount ou atualizar uma existente|
|/apiManagementAccounts/Delete|Excluir uma APIManagementAccount existente|
|/apiManagementAccounts/connectionAcls/Read|Obter lista de saudação de Acls de Conexão.|
|/apiManagementAccounts/apiAcls/Read|Ler ConnectionAcls|
|/connections/Read|Obter lista de saudação de conexões.|
|/connections/Write|Criar ou atualizar uma conexão.|
|/connections/Delete|Excluir uma conexão.|
|/connections/Join/Action|Ingressar em uma conexão.|
|/connections/confirmconsentcode/action|Confirmar o código de autorização de conexões.|
|/connections/listconsentlinks/action|Listar os links de autorização para conexões.|
|/deploymentlocations/read|Obter locais de implantação.|
|/sourcecontrols/read|Obter os controles de origem.|
|/sourcecontrols/write|Atualizar controles de origem.|
|/managedhostingenvironments/read|Obter ambientes de hospedagem gerenciados.|
|/managedhostingenvironments/sites/read|Obter aplicativos Web de ambientes de hospedagem gerenciados.|
|/managedhostingenvironments/serverfarms/read|Obter Planos do Serviço de Aplicativo de ambientes de hospedagem gerenciados.|
|/locations/managedapis/read|Obter as APIs gerenciadas dos locais.|
|/locations/apioperations/read|Obter operações API dos locais.|
|/locations/connectiongatewayinstallations/read|Obter as instalações de gateway de conexão locais.|
|/listSitesAssignedToHostName/Read|Obter os nomes de sites atribuídos toohostname.|

## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[criar uma função personalizada](role-based-access-control-custom-roles.md).

- Saudação de revisão [criados em funções RBAC](role-based-access-built-in-roles.md).

- Saiba como toomanage acessar atribuições [por usuário](role-based-access-control-manage-assignments.md) ou [por recurso](role-based-access-control-configure.md) 
