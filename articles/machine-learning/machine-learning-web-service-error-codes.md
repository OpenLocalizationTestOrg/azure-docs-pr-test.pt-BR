---
title: "códigos de erro de API de REST de aprendizado de máquina aaaAzure | Microsoft Docs"
description: "Esses códigos de erro podem ser retornados por uma operação em um serviço Web do Machine Learning do Azure."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Códigos de Erro da API REST do Machine Learning
 
Olá códigos de erro a seguir podem ser retornados por uma operação em um serviço web de aprendizado de máquina do Azure.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (código de status HTTP 400)
 
Argumento inválido fornecido.
 
Essa classe de erros significa que um argumento fornecido em algum lugar foi inválido. Isso pode ser uma credencial ou um local de armazenamento do Azure toosomething passado toohello serviço de web. Examine o campo de "código de erro" hello em hello "Detalhes" seção toodiagnose que argumento específico era inválido.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| BadParameterValue | valor de parâmetro Hello fornecido não satisfaz a regra de parâmetro hello no parâmetro hello |
| BadSubscriptionId | assinatura de saudação Id tooscore usado não está Olá uma presente no recurso Olá |
| BadVersionCall | Parâmetro de versão inválido foi passado durante a chamada de API de saudação: {0}. Saudação de seleção API ajuda página para passar a versão correta do hello e tente novamente. |
| BatchJobInputsNotSpecified | Olá entradas necessárias a seguir não foram especificada com solicitação Olá: {0}. Verifique se todos os dados de entrada estão especificados e tente novamente. |
| BatchJobInputsTooManySpecified | solicitação de saudação especificada mais entradas que foi definido no serviço de saudação. Lista de entrada(s) aceita(s): {0}. Verifique se todos os dados de entrada estão especificados corretamente e tente de novo. |
| BlobNameTooLong | O caminho do armazenamento de blobs do Azure fornecido para a saída de diagnóstico é muito longo: {0}. Diminuir Olá caminho e tente novamente. |
| BlobNotFound | Não é possível tooaccess Olá fornecido BLOBs do Azure - {0}.  Mensagem de erro do Azure: {1}. |
| ContainerIsEmpty | Nenhum nome de contêiner de armazenamento do Azure foi fornecido. Forneça um nome de contêiner válido e tente novamente. |
| ContainerSegmentInvalid | Nome do contêiner inválido. Forneça um nome de contêiner válido e tente novamente. |
| ContainerValidationFailed | A validação do contêiner de blobs falhou com este erro: {0}. |
| DataTypeNotSupported | Tipo de dados sem suporte fornecido. Forneça o(s) tipo(s) de dados válido(s) e tente novamente. |
| DuplicateInputInBatchCall | solicitação de lote de saudação é inválida. Não é possível especificar único e múltiplo de entrada em Olá mesmo tempo. Remova um desses itens de solicitação de saudação e tente novamente. |
| ExpiryTimeInThePast | Tempo de expiração fornecido está em Olá últimos: {0}. Forneça uma hora de expiração futura em UTC e tente novamente. toonever expirar, defina tooNULL de tempo de expiração. |
| IncompleteSettings | As configurações de diagnóstico estão incompletas. |
| InputBlobRelativeLocationInvalid | Nenhum nome do blob de armazenamento do Azure fornecido. Forneça um nome de blob válido e tente novamente. |
| InvalidBlob | Especificação de blob inválida para o blob: {0}. Verifique se a cadeia de conexão/caminho relativo ou especificação de token de SAS está correta e tente novamente. |
| InvalidBlobConnectionString | Olá a cadeia de caracteres de conexão especificada para um dos blobs de entrada/saída Olá inválido: {0}. Corrija isso e tente novamente. |
| InvalidBlobExtension | Olá referência de blob: {0} tem uma extensão de arquivo inválido ou ausente. O suporte para as extensões de arquivo desse tipo de saída são: "{1}". |
| InvalidInputNames | Nome (s) especificado na solicitação de saudação de entrada de serviço inválido: {0}. . Olá dados de entrada toohello correto as entradas do mapa e tente novamente. |
| InvalidOutputOverrideName | Nome de substituição da saída inválido: {0}. Olá serviço não tem um nó de saída com esse nome. Passe em um toooverride de nome de nó de saída correto (se aplica diferenciação de maiusculas e minúsculas). |
| InvalidQueryParameter | Parâmetro de consulta inválido '{0}'. {1} |
| MissingInputBlobInformation | Informações ausentes do blob de armazenamento do Azure. Forneça uma cadeia de conexão válida e o caminho relativo ou URI e tente novamente. |
| MissingJobId | Nenhuma Id de trabalho fornecida. Id de um trabalho é retornada quando um trabalho foi enviado para Olá primeira vez. Verifique se Olá Id do trabalho está correto e tente novamente. |
| MissingKeys | Nenhuma Chave fornecida ou uma Chave Primária ou Secundária não é fornecida. |
| MissingModelPackage | Nenhuma Id do pacote de modelo ou pacote de modelo fornecido. Forneça uma Id do pacote de modelo válida ou pacote de modelo e tente novamente. |
| MissingOutputOverrideSpecification | solicitação de saudação tem especificação de blob Olá para substituição de saída {0}. . Especifique um local de blob válido com solicitação hello, ou remova a especificação de saída de hello se nenhuma substituição de local é desejada. |
| MissingRequestInput | serviço web de saudação espera uma entrada, mas nenhuma entrada foi fornecida. Verifique se as entradas válidas são fornecidas com base em Olá publicado portas no modelo de saudação de entrada e tente novamente. |
| MissingRequiredGlobalParameters | Nem todos os parâmetros de serviço Web necessários fornecidos. Verifique se os parâmetros de saudação esperado para Olá módulos estão corretas e tente novamente. |
| MissingRequiredOutputOverrides | Ao chamar um ponto de extremidade de serviço criptografada é obrigatório toopass na saída substituições para saídas do serviço Olá todos. Faltam substituições no momento para essas saídas: {0} |
| MissingWebServiceGroupId | Nenhuma Id do grupo de serviços Web fornecida. Forneça uma Id do grupo de serviços Web válida e tente novamente. |
| MissingWebServiceId | Nenhuma Id do serviço Web fornecida. Forneça uma Id do serviço Web válida e tente novamente. |
| MissingWebServicePackage | Nenhum pacote de Serviço Web fornecido. Forneça um pacote de serviço Web válido e tente novamente. |
| MissingWorkspaceId | Nenhuma Id do espaço de trabalho fornecida. Forneça uma Id do espaço de trabalho válida e tente novamente. |
| ModelConfigurationInvalid | Configuração de modelo inválido no pacote de modelo de saudação. Verifique a configuração do modelo de saudação contém a definição de extremidade de saída, ponto de extremidade de erro padrão, e std fora do ponto de extremidade e tente novamente. |
| ModelPackageIdInvalid | Id do pacote do modelo inválida. Verifique se que esse pacote de modelo Olá Id está correto e tente novamente. |
| RequestBodyInvalid | Não há corpo da solicitação fornecida ou erro durante a desserialização do corpo da solicitação hello. |
| RequestIsEmpty | Nenhuma solicitação fornecida. Forneça uma solicitação válida e tente novamente. |
| UnexpectedParameter | Parâmetros inesperados fornecidos. Verifique se todos os nomes de parâmetro estão escritos corretamente, somente os parâmetros esperados são passados e tente novamente. |
| UnknownError | Erro desconhecido. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Não é possível alterar os requisitos de solicitações simultâneas para o serviço Web {0}. |
| WebServiceIdInvalid | Id do serviço Web inválida fornecida. A Id do serviço Web deve ser uma guid válida. |
| WebServiceTooManyConcurrentRequestRequirement | Não é possível definir toomore do requisito de solicitações simultâneas que {0}. |
| WebServiceTypeInvalid | Tipo de serviço Web inválido fornecido. Verifique se o tipo de serviço web válida hello está correto e tente novamente. Tipos de serviço Web válidos: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (código de status HTTP 400)
 
Argumento inválido do usuário fornecido.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| InputMismatchError | Os dados de entrada não coincidem com o esquema da porta de entrada. |
| InputParseError | Falha da análise do vetor de entrada.  Verifique se o vetor de entrada hello tem o número correto de saudação de colunas e tipos de dados.  Detalhes adicionais: {0}. |
| MissingRequiredGlobalParameters | Parâmetro (s) esperado pelo serviço da web de saudação está ausentes. Verifique se todos os parâmetros de saudação necessário esperados pelo serviço da web de saudação estão corretos e tente novamente. |
| UnexpectedParameter | Verificar somente Olá necessários parâmetros esperados pelo serviço da web de saudação são passados e tente novamente. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (código de status HTTP 400)
 
solicitação de saudação é inválida no contexto atual de saudação.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| CannotStartJob | trabalho de saudação não pode ser iniciado porque ele está em estado {0}. |
| IncompatibleModel | modelo de saudação é incompatível com a versão de solicitação de saudação. versão de solicitação Olá só oferece suporte a modelos de saída única datatable. |
| MultipleInputsNotAllowed | modelo de saudação não permite que várias entradas. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (código de status HTTP 400)
 
A execução do módulo encontrou um erro interno de biblioteca.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (código de status HTTP 400)
 
A execução do módulo encontrou um erro.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (código de status HTTP 400)
 
Pacote de serviço Web inválido. Verifique se o pacote de serviço da web hello fornecido está correto e tente novamente.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| FormatError | pacote de serviço da web Hello está malformado. Detalhes: {0} |
| RuntimesError | gráfico de pacote de serviço Olá web é inválido. Detalhes: {0} |
| ValidationError | gráfico de pacote de serviço Olá web é inválido. Detalhes: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Não autorizado (código de status HTTP 401)
 
Solicitação é tooaccess não autorizado de recursos.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| AdminRequestUnauthorized | Não Autorizado |
| ManagementRequestUnauthorized | Não Autorizado |
| ScoreRequestUnauthorized | Credenciais inválidas fornecidas. |
 
## <a name="notfound-http-status-code-404"></a>Não Encontrado (código de status HTTP 404)
 
Recurso não encontrado.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| ModelPackageNotFound | Pacote do modelo não encontrado. Verifique se o pacote de modelo Olá Id está correta e tente novamente. |
| WebServiceIdNotFoundInWorkspace | Serviço Web nesse espaço de trabalho não encontrado. Há uma incompatibilidade entre Olá webServiceId e workspaceId Olá. Verifique se o serviço web de saudação fornecido é parte do espaço de trabalho hello e tente novamente. |
| WebServiceNotFound | Serviço Web não encontrado. Verifique se o serviço web de saudação Id está correta e tente novamente. |
| WorkspaceNotFound | Espaço de trabalho não encontrado. Verifique se o espaço de trabalho Olá Id está correta e tente novamente. |
 
## <a name="requesttimeout-http-status-code-408"></a>Tempo Limite da Solicitação (código de status HTTP 408)
 
não foi possível concluir a operação de saudação no hello permitido de tempo.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| RequestCanceled | Solicitação cancelada pelo cliente hello. |
| ScoreRequestTimeout | Tempo limite da solicitação de execução. |
 
## <a name="conflict-http-status-code-409"></a>Conflito (código de status HTTP 409)
 
O recurso já existe.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Nome do parâmetro de saída inválido. Olá metadados editor módulo toorename colunas e tente novamente. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>Violação da Cota de Memória (código de status HTTP 413)
 
modelo de saudação tinha excedeu a cota de memória de saudação atribuída tooit.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| OutOfMemoryLimit | modelo de saudação consumido mais memória do que foi apropriados para ele. Máximo de memória permitido para o modelo de saudação é {0} MB. Verifique seu modelo quanto a problemas. |
 
## <a name="internalerror-http-status-code-500"></a>Erro Interno (código de status HTTP 500)
 
A execução encontrou um erro interno.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | processo do contêiner Olá falhou com erro do sistema |
| ContainerProcessTerminatedWithUnknownError | processo do contêiner Olá falhou com erro desconhecido |
| ContainerValidationFailed | A validação do contêiner de blobs falhou com este erro: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Nenhum argumento fornecido. Verifique se os argumentos válidos são passados e tente novamente. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Id da porta={0} tem um tipo de dados sem suporte: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Falha na geração do Swagger, Detalhes: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Código de status do trabalho desconhecido {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, Detalhes: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (código de status HTTP 500)
 
A execução encontrou um erro interno. Sistema com memória insuficiente. Tente novamente.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (código de status HTTP 500)
 
Pacote do modelo inválido. Verifique se o pacote de modelo Olá fornecido está correto e tente novamente.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (código de status HTTP 500)
 
Pacote de serviço Web inválido. Verifique se o pacote de web hello fornecido está correto e tente novamente.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| ModuleError | gráfico de pacote de serviço Olá web é inválido. Detalhes: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (código de status HTTP 503)
 
não é possível executar solicitação Hello como Olá contêineres estão sendo inicializados.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (código de status HTTP 503)
 
O serviço está temporariamente indisponível.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| NoMoreResources | Nenhum recurso disponível para a solicitação. |
| RequestThrottled | A solicitação foi restringida para o ponto de extremidade {0}. simultaneidade de saudação máximo para o ponto de extremidade de saudação é \\{1 \\}. |
| TooManyConcurrentRequests | Muitas solicitações simultâneas enviadas. |
| TooManyHostsBeingInitialized | Muitos hosts que está sendo inicializados no hello mesmo tempo. Considere limitar/tentar novamente. |
| TooManyHostsBeingInitializedPerModel | Muitos hosts que está sendo inicializados no hello mesmo tempo. Considere limitar/tentar novamente. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>Tempo Limite do Gateway (código de status HTTP 504)
 
não foi possível concluir a operação de saudação no hello permitido de tempo.
 
| Código do erro | Mensagem do usuário |
| ---------- |--------------|
| BackendInitializationTimeout | não foi possível concluir a inicialização do serviço da web Hello dentro Olá permitido de tempo. |
| BackendScoreTimeout | não foi possível concluir a execução de solicitação de serviço web Hello dentro Olá permitido de tempo. |
 
