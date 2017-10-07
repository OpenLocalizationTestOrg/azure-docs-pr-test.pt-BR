---
title: aaaPowerShell conector | Microsoft Docs
description: Este artigo descreve como o conector do Microsoft tooconfigure do Windows PowerShell.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Referência técnica do Windows PowerShell Connector
Este artigo descreve Olá conector do Windows PowerShell. artigo Olá aplica toohello produtos a seguir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * É necessário usar o hotfix 4.1.3671.0 ou posterior [KB3092178](https://support.microsoft.com/kb/3092178).

Para MIM2016 e FIM2010R2, Olá Connector está disponível como um download do hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Visão geral da saudação conector do PowerShell
Olá PowerShell conector permite serviço de sincronização de saudação toointegrate com sistemas externos que oferecem que APIs baseadas no Windows PowerShell. conector de saudação fornece uma ponte entre recursos Olá Olá conectividade extensível baseada em chamada do agente de gerenciamento 2 framework (ECMA2) e do Windows PowerShell. Para obter mais informações sobre a estrutura ECMA hello, consulte Olá [extensível conectividade 2.2 Management Agent referência](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar o conector de saudação, verifique se que você tem o seguinte Olá no servidor de sincronização de saudação:

* Microsoft .NET 4.5.2 Framework ou posterior
* Windows PowerShell 2.0, 3.0 ou 4.0

política de execução Olá no servidor do serviço de sincronização de saudação deve ser configurado tooallow Olá conector toorun do Windows PowerShell scripts. A menos que a execução do conector de Olá Olá scripts assinadas digitalmente, configure a política de execução de saudação executando este comando:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Criar um novo conector
toocreate um conector do Windows PowerShell no serviço de sincronização de saudação, você deve fornecer uma série de scripts do Windows PowerShell que execute as etapas de saudação solicitadas pelo serviço de sincronização de saudação. Dependendo da fonte de dados Olá você conectar-se a funcionalidade de saudação tooand necessária, scripts de saudação, você deve implementar varia. Esta seção descreve cada um dos scripts de saudação que podem ser implementados e quando eles são necessários.

Olá, o Windows PowerShell conector é projetado toostore scripts hello dentro do banco de dados de serviço de sincronização de saudação. Embora seja possível toorun scripts que são armazenados no sistema de arquivo hello, é mais fácil corpo de saudação tooinsert cada script diretamente na configuração do conector toohello.

tooCreate um conector do PowerShell, no **serviço de sincronização** selecione **Management Agent** e **criar**. Selecione Olá **PowerShell (Microsoft)** conector.

![Criar o conector](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Conectividade
Forneça os parâmetros de configuração para conectar-se o sistema remoto tooa. Esses valores são armazenados por Olá serviço de sincronização e feitos tooyour disponíveis do Windows PowerShell scripts quando Olá conector é executado com segurança.

![Conectividade](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Você pode configurar Olá parâmetros de conectividade a seguir:

**Conectividade**

| Parâmetro | Valor Padrão | Finalidade |
| --- | --- | --- |
| Servidor |<Blank> |Nome do servidor que Olá conector deve se conectar ao. |
| Domínio |<Blank> |Domínio da saudação toostore de credencial para uso ao conector de saudação é executado. |
| Usuário |<Blank> |Nome de usuário da saudação toostore de credencial para uso ao conector de saudação é executado. |
| Senha |<Blank> |Senha da saudação toostore de credencial para uso ao conector de saudação é executado. |
| Representar Conta do Conector |Falso |Quando for verdadeiro, serviço de sincronização de saudação executa scripts do Windows PowerShell Olá no contexto Olá Olá credenciais fornecidas. Quando possível, é recomendável que Olá **$Credentials** parâmetro é passado tooeach script é usado em vez de representação. Para obter mais informações sobre permissões adicionais que são necessárias toouse essa opção, consulte [configuração adicional para representação](#additional-configuration-for-impersonation). |
| Carregar o Perfil de Usuário ao Representar |Falso |Instrui o perfil de usuário do Windows tooload Olá de credenciais do conector Olá durante a representação. Se o usuário representado Olá tem um perfil móvel, conector Olá não carrega o perfil móvel hello. Para obter mais informações sobre permissões adicionais que são necessárias toouse esse parâmetro, consulte [configuração adicional para representação](#additional-configuration-for-impersonation). |
| Tipo de Logon ao Representar |Nenhum |Tipo de logon durante representação. Para obter mais informações, consulte Olá [dwLogonType] [ dw] documentação. |
| Somente Scripts Assinados |Falso |Se true, conector do Windows PowerShell Olá valida cada script possui uma assinatura digital válida. Se for false, certifique-se de que a política de execução do servidor do serviço de sincronização de saudação do Windows PowerShell é RemoteSigned ou irrestrito. |

**Módulo Comum**  
Olá conector permite que você toostore um módulo do Windows PowerShell compartilhado na configuração de saudação. Quando o conector Olá executa um script, hello módulo do Windows PowerShell extraídos toohello sistema de arquivos para que ele possa ser importado por cada script.

Para scripts de importação, exportação e a sincronização de senha, módulo comum Olá é pasta de MAData toohello extraídos do conector. Para scripts de descoberta de esquema, validação, hierarquia e partição módulo comum Olá é pasta extraída toohello % TEMP %. Em ambos os casos, Olá extraídos comuns módulo de script é nomeado de acordo com a configuração de nome de Script de módulo comum toohello.

tooload um módulo chamado FIMPowerShellConnectorModule.psm1 da pasta de MAData hello, use Olá instrução a seguir:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload um módulo chamado FIMPowerShellConnectorModule.psm1 da pasta Olá % TEMP %, use Olá instrução a seguir:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Validação de Parâmetro**  
Olá Script de validação é um script do Windows PowerShell opcional que pode ser usado tooensure que parâmetros de configuração de conector fornecidos pelo administrador de saudação são válidos. O servidor de validação, credenciais de conexão e parâmetros de conectividade são os usos comuns do script de validação de saudação. script de validação Hello é chamado depois hello guias e caixas de diálogo a seguir são modificadas:

* Conectividade
* Parâmetros Globais
* Configuração de Partição

script de validação Olá recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |Guia de configuração de saudação ou caixa de diálogo que disparou a solicitação de validação de saudação. |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |

script de validação Olá deve retornar um único pipeline de toohello do objeto ParameterValidationResult.

**Descoberta de Esquema**  
Olá script de descoberta de esquema é obrigatório. Esse script retorna tipos de objeto hello, atributos e restrições de atributo que Olá que usa o serviço de sincronização ao configurar regras de fluxo de atributo. Olá script de descoberta de esquema é executado durante a criação do conector e preenche o esquema do conector hello. Ele também é usado por Olá ação Atualizar esquema Olá Synchronization Service Manager.

script de descoberta de esquema Olá recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |

script Hello deve retornar um único [esquema] [ schema] pipeline de toohello do objeto. objeto de esquema de saudação é composto de [SchemaType] [ schemaT] objetos que representam os tipos de objeto (por exemplo: usuários e grupos). objeto de SchemaType Olá contém uma coleção de [SchemaAttribute] [ schemaA] objetos que representam atributos de saudação (por exemplo: nome, sobrenome e endereço postal) do tipo hello.

**Parâmetros Adicionais**  
Além disso configurações padrão de toohello, você pode definir as configurações personalizadas adicionais instância toohello específico de saudação conector. Esses parâmetros podem ser especificados no conector hello, partição, ou a etapa de execução níveis e acessado a partir do script do Windows PowerShell relevante de saudação. Configurações personalizadas podem ser armazenadas no banco de dados de serviço de sincronização de saudação em texto sem formatação ou eles podem ser criptografados. Olá serviço de sincronização automaticamente criptografa e descriptografa as definições de configuração segura quando necessário.

toospecify configurações personalizadas, nome hello separado de cada parâmetro com uma vírgula (,).

tooaccess configurações personalizadas de um script, você deve sufixo nome hello com um sublinhado ( \_ ) e o escopo de saudação do parâmetro hello (Global, partição ou RunStep). Por exemplo, tooaccess Olá parâmetro FileName Global, use este trecho de código:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Funcionalidades
Guia de recursos de saudação do hello Designer do agente de gerenciamento define o comportamento de saudação e a funcionalidade do conector de saudação. as seleções de saudação nessa guia não podem ser modificadas quando Olá conector foi criado. Esta tabela lista as configurações de recurso de saudação.

![Funcionalidades](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Recurso | Descrição |
| --- | --- |
| [Estilo de Nome Diferenciado][dnstyle] |Indica se conector Olá dá suporte a nomes distintos e, portanto, o estilo. |
| [Tipo de Exportação][exportT] |Determina o tipo de saudação de objetos que são apresentados toohello script de exportação. <li>AttributeReplace – inclui todo o conjunto de valores para um atributo com vários valores hello quando o atributo de saudação é alterado.</li><li>AttributeUpdate – inclui somente Olá deltas tooa múltiplos atributo quando o atributo de saudação é alterado.</li><li>MultivaluedReferenceAttributeUpdate - inclui um conjunto completo de valores de atributos de vários valores de não referência e apenas deltas para atributos de referência com vários valores.</li><li>ObjectReplace – inclui todos os atributos de um objeto quando qualquer atributo é alterado</li> |
| [Normalização de Dados][DataNorm] |Instrui a atributos de âncora de toonormalize de serviço de sincronização de saudação antes que eles são fornecidos tooscripts. |
| [Confirmação do Objeto][oconf] |Configura Olá pendentes comportamento de importação em Olá serviço de sincronização. <li>Normal – comportamento padrão que espera todas exportadas toobe alterações confirmada através da importação</li><li>NoDeleteConfirmation – quando um objeto é excluído, não há nenhuma importação pendente gerada.</li><li>NoAddAndDeleteConfirmation – quando um objeto é criado ou excluído, não há nenhuma importação pendente gerada.</li> |
| Usar DN como âncora |Se hello estilo de nome diferenciado é definido tooLDAP, atributo de âncora Olá para o espaço do conector Olá também será nome distinto hello. |
| Operações Simultâneas de Vários Conectores |Quando marcada, vários conectores do Windows PowerShell podem ser executados simultaneamente. |
| Partições |Quando marcada, o conector Olá dá suporte a várias partições e descoberta da partição. |
| Hierarquia |Quando marcada, o conector Olá dá suporte a uma estrutura hierárquica de estilo do LDAP. |
| Habilitar Importação |Quando marcada, o conector de saudação importa dados por meio de scripts de importação. |
| Habilitar Importação Delta |Quando marcada, o conector Olá pode solicitar deltas de saudação importar scripts. |
| Habilitar Exportação |Quando marcada, o conector Olá exporta dados por meio de scripts de exportação. |
| Habilitar Exportação Completa |Quando marcada, Olá exportar exportando espaço do conector inteiro Olá suporte a scripts. toouse que essa opção, habilitar a exportação também deve ser verificada. |
| Nenhum Valor de Referência na Primeira Passagem de Exportação |Quando marcada, os atributos de referência são exportados em uma segunda passagem de exportação. |
| Habilitar Renomeação do Objeto |Quando marcada, os nomes diferenciados podem ser modificados. |
| Excluir-Adicionar como Substituição |Quando marcada, as operações excluir-adicionar são exportadas como uma única substituição. |
| Habilitar Operações de Senha |Quando marcada, há suporte para scripts de sincronização de senha. |
| Habilitar Exportar Senha na Primeira Passagem |Quando marcada, senhas definidas durante o provisionamento são exportadas quando Olá objeto é criado. |

### <a name="global-parameters"></a>Parâmetros Globais
guia parâmetros globais Olá Olá Management Agent Designer permite tooconfigure saudação do Windows PowerShell scripts que são executados pelo conector hello. Você também pode configurar valores globais para configurações personalizadas definidas na guia de conectividade de saudação.

**Descoberta de Partição**  
Uma partição é um namespace separado dentro de um esquema compartilhado. Por exemplo, no Active Directory, cada domínio é uma partição em uma floresta. Uma partição é um agrupamento lógico de saudação para importação e exportação de operações. Importação e Exportação têm partição como um contexto e todas as operações ocorrem nesse contexto. Partições devem toorepresent uma hierarquia no LDAP. nome distinto de saudação de uma partição é usado na importação tooverify todos os retornados os objetos estão dentro do escopo de saudação de uma partição. nome diferenciado da partição Olá também é usado durante o provisionamento de saudação metaverso toohello conector espaço toodetermine Olá partição que deve ser associado a um objeto durante a exportação.

script de descoberta de partição Olá recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |

Olá script deve retornar um uma única [partição] [ part] objeto ou uma lista [T] do pipeline de toohello de objetos de partição.

**Descoberta de Hierarquia**  
script de descoberta de hierarquia Olá é usado somente quando Olá recurso de estilo de nome diferenciado é LDAP. script Hello é usado tooallow você toobrowse e selecione um conjunto de contêineres que é considerado em ou fora do escopo de importação e exportação de operações. script Hello só deve fornecer uma lista de nós que são filhos diretos de saudação raiz nó fornecido toohello script.

script de descoberta de hierarquia Olá recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| ParentNode |[HierarchyNode][hn] |nó de raiz de saudação da hierarquia de saudação em qual Olá script deve retornar os filhos diretos. |

script Hello deve retornar um objeto de HierarchyNode um único filho ou uma lista [T] do pipeline de toohello de objetos filho HierarchyNode.

#### <a name="import"></a>Importar
Os conectores que oferecem suporte às operações de importação devem implementar três scripts.

**Iniciar Importação**  
Olá começar a importar script é executado no início de uma etapa de importação executar hello. Durante esta etapa, você poderá estabelecer um sistema de origem de toohello de conexão e fazer as etapas preparatórias antes de importar dados de saudação sistema conectado.

Olá começar a importar script recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa o script hello sobre tipo de saudação de importação executar (completo ou delta), partição, hierarquia, marca d'água e tamanho de página esperado. |
| Tipos |[Schema][schema] |Esquema para o espaço do conector Olá que é importado. |

script Hello deve retornar um único [OpenImportConnectionResults] [ oicres] objeto pipeline toohello, por exemplo:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Importar Dados**  
script de importação de dados de saudação é chamado pelo conector Olá até que o script hello indica que não há nenhuma mais tooimport de dados. conector do Windows PowerShell Olá tem um tamanho de página de 9.999 objetos. Se o script retornar mais de 9.999 objetos para importação, você deverá dar suporte à paginação. expõe de conector Olá uma propriedade de dados personalizados que você pode usar o repositório de tooa uma marca d'água para que cada Olá tempo Importar script de dados é chamada, o script continua a importação de objetos de onde parou.

script de importação de dados de saudação recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Mantém Olá marca d'água (CustomData) que pode ser usada durante importações pagináveis e importa delta. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa o script hello sobre tipo de saudação de importação executar (completo ou delta), partição, hierarquia, marca d'água e tamanho de página esperado. |
| Tipos |[Schema][schema] |Esquema para o espaço do conector Olá que é importado. |

Olá script de importação de dados deve gravar uma lista [[CSEntryChange][csec]] pipeline de toohello do objeto. Essa coleção é composta por atributos CSEntryChange que representam cada objeto que está sendo importado. Durante uma importação completa, essa coleção deve ter um conjunto completo de objetos CSEntryChange que tenham todos os atributos para cada objeto. Durante a importação de Delta, objeto de CSEntryChange Olá deve conter deltas de nível de atributo Olá para cada tooimport de objeto ou uma representação completa de objetos de saudação que foram alterados (modo de substituição).

**Encerrar Importação**  
Na conclusão de saudação da importação de saudação executar, Olá final Importar script é executado. Esse script deve executar as tarefas de limpeza necessárias (por exemplo, encerre as conexões toosystems e responder toofailures).

script de importação de término Hello recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa o script hello sobre tipo de saudação de importação executar (completo ou delta), partição, hierarquia, marca d'água e tamanho de página esperado. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Informa o script hello sobre motivo Olá importação Olá foi finalizada. |

script Hello deve retornar um único [CloseImportConnectionResults] [ cicres] objeto pipeline toohello, por exemplo:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Exportação
Arquitetura de importação toohello idênticas do conector Olá, os conectores que oferece suporte à exportação devem implementar três scripts.

**Iniciar Importação**  
Olá iniciar exportação script é executado no início de saudação de uma etapa de execução de exportação. Durante esta etapa, você pode estabelecer um sistema de origem de toohello de conexão e realize as etapas preparatórias antes de exportar dados toohello sistema conectado.

Olá iniciar exportação script recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa o script hello sobre tipo hello de execução de exportação (completo ou delta), partição, hierarquia e tamanho de página esperado. |
| Tipos |[Schema][schema] |Esquema para o espaço do conector Olá exportado. |

script Hello não deve retornar qualquer pipeline toohello de saída.

**Exportar Dados**  
Olá serviço de sincronização chama o script de exportar dados de saudação quantas vezes for necessário tooprocess todas as exportações pendentes. Se o espaço do conector Olá tem mais exportações pendentes que o tamanho da página do conector de hello, exportação Olá script de dados pode ser chamado várias vezes e possivelmente várias vezes para Olá mesmo objeto.

script de exportação de dados de saudação recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| CSEntries |IList[CSEntryChange][csec] |Lista de todos os espaços de conector Olá objetos com pendente toobe exportações processada durante essa passagem. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa o script hello sobre tipo hello de execução de exportação (completo ou delta), partição, hierarquia e tamanho de página esperado. |
| Tipos |[Schema][schema] |Esquema para o espaço do conector Olá exportado. |

Olá script de exportação de dados deve retornar um [PutExportEntriesResults] [ peeres] pipeline de toohello do objeto. Este objeto não precisa de informações de resultado de tooinclude para cada conector exportado a menos que ocorra um erro ou um atributo de âncora de toohello de alteração. Por exemplo, tooreturn um pipeline de toohello PutExportEntriesResults objeto:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Encerrar Exportação**  
Na conclusão de saudação da exportação de saudação é executado, Olá final exportar toorun de script. Esse script deve executar as tarefas de limpeza necessárias (por exemplo, encerre as conexões toosystems e responder toofailures).

script de exportação de término Hello recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa o script hello sobre tipo hello de execução de exportação (completo ou delta), partição, hierarquia e tamanho de página esperado. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Informa o script hello sobre motivo Olá exportação Olá foi finalizada. |

script Hello não deve retornar qualquer pipeline toohello de saída.

#### <a name="password-synchronization"></a>Sincronização de senha
Os conectores do Windows PowerShell podem ser usados como um destino para alterações/redefinições de senha.

script de senha Olá recebe Olá parâmetros a seguir do conector hello:

| Nome | Tipo de Dados | Descrição |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabela de parâmetros de configuração para Olá conector. |
| Credencial |[PSCredential][pscred] |Contém as credenciais inseridas pelo administrador Olá na guia de conectividade de saudação. |
| Partition |[Partição][part] |Partição de diretório que Olá CSEntry está em. |
| CSEntry |[CSEntry][cse] |Entrada de espaço do conector para objeto Olá recebeu uma alteração de senha ou redefinido. |
| OperationType |Cadeia de caracteres |Indica se a operação de saudação é uma redefinição (**SetPassword**) ou uma alteração (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Sinalizadores que especificam Olá destinado comportamento de redefinição de senha. Esse parâmetro estará disponível somente se OperationType for **SetPassword**. |
| OldPassword |Cadeia de caracteres |Preenchido com a senha antiga do objeto Olá para alterações de senha. Esse parâmetro estará disponível somente se OperationType for **ChangePassword**. |
| NewPassword |Cadeia de caracteres |Preenchido com a nova senha do objeto Olá que deve ser definidos por script hello. |

Olá script de senha é qualquer pipeline do Windows PowerShell de toohello resultados de tooreturn não esperado. Se ocorrer um erro no script de senha hello, script hello deve lançar uma saudação exceções tooinform Olá serviço de sincronização sobre problema Olá a seguir:

* [PasswordPolicyViolationException] [ pwdex1] – lançada se senha Olá não atender a política de senha Olá no sistema Olá conectado.
* [PasswordIllFormedException] [ pwdex2] – lançada se Olá senha não é aceitável para o sistema Olá conectado.
* [PasswordExtension] [ pwdex3] – lançada para todos os outros erros no script de senha hello.

## <a name="sample-connectors"></a>Conectores de exemplo
Para obter uma visão geral completa dos conectores do exemplo disponível hello, consulte [coleção de conector de exemplo do Windows PowerShell conector][samp].

## <a name="other-notes"></a>Outras observações
### <a name="additional-configuration-for-impersonation"></a>Configuração adicional para representação
Conceder saudação do usuário que é representada hello seguintes permissões no servidor do serviço de sincronização de saudação:

Acesso de leitura toohello de chaves do registro a seguir:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

Olá toodetermine identificador de segurança (SID) da conta de serviço do serviço de sincronização hello, executar Olá comandos do PowerShell a seguir:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Acesso de leitura toohello de pastas do sistema de arquivos a seguir:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Substitua o nome de saudação do conector do Windows PowerShell de saudação de espaço reservado de Olá {ConnectorName}.

## <a name="troubleshooting"></a>Solucionar problemas
* Para obter informações sobre como o log tooenable tootroubleshoot Olá conector, consulte Olá [como tooEnable o rastreamento ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
