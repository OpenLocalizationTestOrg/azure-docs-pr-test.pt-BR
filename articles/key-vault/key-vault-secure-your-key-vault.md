---
title: aaaSecure sua chave de cofre | Microsoft Docs
description: "Gerencie permissões de acesso para o cofre de chaves para gerenciar cofres, chaves e segredos. Modelo de autenticação e autorização para o Cofre de chaves e como toosecure sua chave de cofre"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Proteger seu cofre de chaves
O Cofre de Chaves do Azure é um serviço de nuvem que protege chaves de criptografia e segredos (como certificados, cadeias de conexão e senhas) para aplicativos de nuvem. Como esses dados são confidenciais e críticos de negócios, você deseja cofres de chaves toosecure acesso tooyour autorizadas apenas aplicativos e os usuários podem acessar o Cofre de chaves. Este artigo fornece uma visão geral do modelo de Cofre de chaves de acesso, explica a autenticação e autorização e descreve como toosecure acesso tookey cofre para seus aplicativos de nuvem com um exemplo.

## <a name="overview"></a>Visão geral
Cofre de chaves de tooa de acesso é controlado por meio de duas interfaces separadas: plano de gerenciamento e de dados. Para ambos os planos de autorização e autenticação adequada é necessária antes de um chamador (um usuário ou um aplicativo) pode obter cofre tookey de acesso. Autenticação estabelece a identidade de saudação do chamador hello, enquanto a autorização determina quais chamador de saudação de operações é permitido tooperform.

Para a autenticação, o plano de gerenciamento e o plano de dados usam o Azure Active Directory. Para a autorização, o plano de gerenciamento usa RBAC (controle de acesso baseado em função), enquanto o plano de dados usa a política de acesso do cofre de chaves.

Aqui está uma breve visão geral dos tópicos de saudação abordados:

[A autenticação usando o Active Directory do Azure](#authentication-using-azure-active-directory) -esta seção explica como um chamador autenticado com o Active Directory do Azure tooaccess um cofre de chaves por meio do plano de gerenciamento e de dados. 

[Plano de gerenciamento e plano de dados](#management-plane-and-data-plane) - o plano de gerenciamento e o plano de dados são dois planos de acesso usados para acessar o cofre de chaves. Cada plano de acesso dá suporte a operações específicas. Esta seção descreve os pontos de extremidade de acesso hello, operações com suporte e acessar o método de controle usado por cada plano. 

[Controle de acesso do plano de gerenciamento](#management-plane-access-control) - nesta seção, examinaremos permitindo acesso toomanagement operações de plano usando o controle de acesso baseado em função.

[Controle de acesso do plano de dados](#data-plane-access-control) -esta seção descreve como os dados de toocontrol toouse Cofre de chaves acesso política plano acesso.

[Exemplo](#example) -Este exemplo descreve como o controle para seu Cofre de chaves tooallow três diferentes equipes (equipe de segurança, os desenvolvedores/operadores e auditores) de acesso toosetup tooperform toodevelop de tarefas específicas, gerenciar e monitorar um aplicativo no Azure .

## <a name="authentication-using-azure-active-directory"></a>Autenticação usando o Azure Active Directory
Quando você criar um cofre de chaves em uma assinatura do Azure, é automaticamente associado ao locatário do Azure Active Directory da assinatura hello. Todos os chamadores (usuários e aplicativos) devem ser registrado no tooaccess locatário este cofre de chaves. Um aplicativo ou um usuário deve ser autenticado com o Cofre de chaves de tooaccess do Active Directory do Azure. Isso se aplica a tooboth plano de gerenciamento e de dados access. Em ambos os casos, um aplicativo pode acessar o cofre de chaves de duas maneiras:

* **acesso de usuário+aplicativo** - geralmente isso é para aplicativos que acessam o cofre de chaves em nome de um usuário conectado. O Azure PowerShell e o Portal do Azure são exemplos desse tipo de acesso. Há duas maneiras toogrant acesso toousers: unidirecional é toogrant toousers de acesso para que possam acessar o Cofre de chaves de qualquer aplicativo e Olá outra forma é toogrant um cofre de tookey de acesso de usuário somente quando eles usam um aplicativo específico (chamado tooas identidade composta). 
* **acesso somente de aplicativo** - para aplicativos que executar os serviços de daemon, os trabalhos em segundo plano é concedida a identidade do aplicativo hello etc. acessar toohello cofre da chave.

Em ambos os tipos de aplicativos, aplicativo hello autentica com o Azure Active Directory usando qualquer um dos Olá [métodos de autenticação com suporte](../active-directory/active-directory-authentication-scenarios.md) e adquire um token. Método de autenticação usado depende do tipo de aplicativo hello. Em seguida, o aplicativo hello usa esse token e envia o Cofre de tookey de solicitação de API REST. No caso de saudação de acesso do plano de gerenciamento solicitações são roteadas por meio do ponto de extremidade do Gerenciador de recursos do Azure. Ao acessar dados, aplicativos de saudação fala diretamente o ponto de extremidade do tooa Cofre de chaves. Veja mais detalhes sobre Olá [fluxo de autenticação todo](../active-directory/active-directory-protocols-oauth-code.md). 

nome do recurso Olá para o qual o aplicativo hello solicita um token é diferente dependendo se o aplicativo hello está acessando o plano de gerenciamento ou plano de dados. Portanto, o nome do recurso de Olá é um plano ou dados plano extremidade de gerenciamento descrita na tabela de saudação em uma seção posterior, dependendo do ambiente do Azure de saudação.

Plano de gerenciamento e de dados com um único mecanismo para autenticação tooboth tem seus próprio benefícios:

* As organizações podem controlar centralmente o acesso tooall chave cofres em sua organização
* Se um usuário deixar, eles instantaneamente perdem o acesso tooall cofres de chaves na organização Olá
* As organizações podem personalizar opções de saudação no Azure Active Directory (por exemplo, habilitar autenticação de vários fatores para aumentar a segurança) de autenticação

## <a name="management-plane-and-data-plane"></a>Plano de gerenciamento e plano de dados
O Cofre de Chaves do Azure é um serviço do Azure disponível por meio do modelo de implantação do Azure Resource Manager. Ao criar um cofre de chaves, você obtém um contêiner virtual no qual pode criar outros objetos, como chaves, segredos e certificados. Em seguida, você pode acessar seu Cofre de chaves usando o plano e dados plano tooperform específicas operações de gerenciamento. Interface de gerenciamento do plano é usado toomanage sua chave de cofre em si, como criar, excluir, atualizar os atributos de Cofre de chaves e políticas de acesso para o plano de dados de configuração. Interface de plano de dados é usado tooadd, excluir, modificar e usar chaves hello, segredos e certificados armazenados em seu Cofre de chaves.

interfaces de plano Olá gerenciamento plano e os dados são acessados por meio de pontos de extremidade diferentes (consulte a tabela). a segunda coluna Olá na tabela Olá descreve nomes DNS Olá esses pontos de extremidade em diferentes ambientes do Azure. terceira coluna de saudação descreve as operações de saudação, que você pode executar de cada plano de acesso. Cada plano de acesso também tem seu próprio mecanismo de controle de acesso: para o plano de gerenciamento, o controle de acesso é definido usando o RBAC do Azure Resource Manager (Controle de Acesso Baseado em Função), enquanto para o plano de dados, o controle de acesso é definido usando a política de acesso do cofre de chaves.

| Plano de acesso | Pontos de extremidade de acesso | Operações | Mecanismo de controle de acesso |
| --- | --- | --- | --- |
| Plano de gerenciamento |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure Governo dos EUA:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> management.microsoftazure.de:443 |Criar/Ler/Atualizar/Excluir cofre de chaves <br> Definir políticas de acesso para o cofre de chaves<br>Definir marcas para o cofre de chaves |RBAC (Controle de Acesso Baseado em Função) do Azure Resource Manager |
| Plano de dados |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure Governo dos EUA:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |Para chaves: Descriptografar, Criptografar, UnwrapKey, WrapKey, Verificar, Entrar, Obter, Listar, Atualizar, Criar, Importar, Excluir, Backup, Restauração<br><br> Para segredos: Obter, Listar, Definir, Excluir |Política de acesso do cofre de chaves |

Olá gerenciamento plano e dados plano controles de acesso trabalhar de forma independente. Por exemplo, se você quiser toogrant um chaves de toouse de acesso do aplicativo em um cofre de chaves, basta toogrant permissões de acesso de dados plano usando políticas de acesso do Cofre de chaves e nenhum acesso de plano de gerenciamento é necessária para este aplicativo. E, por outro lado, se você quiser que um usuário toobe capaz de tooread cofre marcas e propriedades, mas não tem qualquer acesso tookeys, segredos ou certificados, você pode conceder a este usuário, é necessário ter acesso de 'leitura' usando o RBAC e nenhum plano de toodata de acesso.

## <a name="management-plane-access-control"></a>Controle de acesso do plano de gerenciamento
plano de gerenciamento de saudação consiste em operações que afetam o Cofre de chaves de saudação em si. Por exemplo, você pode criar ou excluir um cofre de chaves. Você pode obter uma lista de cofres em uma assinatura. Você pode recuperar propriedades de Cofre de chaves (como SKU, tags) e definir políticas de acesso que controlam usuários hello e aplicativos que podem acessar as chaves e segredos no cofre de chaves de saudação de Cofre de chaves. O controle de acesso do plano de gerenciamento usa RBAC. Consulte Olá a lista completa de operações do Cofre de chaves que podem ser executadas por meio do plano de gerenciamento na tabela Olá anterior seção. 

### <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Cada assinatura do Azure tem um Azure Active Directory. Usuários, grupos e aplicativos a partir desse diretório podem ser concedidos acessar toomanage recursos em Olá assinatura do Azure que usam o modelo de implantação do Azure Resource Manager hello. Esse tipo de controle de acesso é tooas chamado controle de acesso baseado em função (RBAC). toomanage acessar, você pode usar o hello [portal do Azure](https://portal.azure.com/), Olá [ferramentas CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [APIs de REST do Azure Resource Manager](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Para criar seu Cofre de chaves em um recurso grupo e controle de acesso toohello plano de gerenciamento do cofre chave com o modelo do Azure Resource Manager hello, usando o Active Directory do Azure. Por exemplo, você pode conceder a usuários ou um cofres de chave de toomanage de capacidade de grupo em um grupo de recursos específicos.

Você pode conceder acesso toousers, grupos e aplicativos em um escopo específico atribuindo funções RBAC apropriadas. Por exemplo, toogrant acessar tooa usuário toomanage chave cofres, você atribui um função predefinida 'chave cofre Colaborador' toothis usuário em um escopo específico. escopo de saudação nesse caso seria uma assinatura, um grupo de recursos ou apenas um cofre de chaves específico. Uma função atribuída no nível de assinatura se aplica a grupos de recursos tooall e recursos na assinatura. Uma função atribuída no nível do grupo de recursos se aplica a recursos tooall desse grupo de recursos. Uma função atribuída a um recurso específico só se aplica a recursos toothat. Há várias funções predefinidas (consulte [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md)), e se Olá funções predefinidas não se ajustam às suas necessidades, você também pode definir suas próprias funções.

> [!IMPORTANT]
> Observe que se um usuário tiver um plano de gerenciamento do Cofre de chaves do Colaborador permissões (RBAC) tooa, ela pode conceder nenhum plano de toodata de acesso, definindo a política de acesso do Cofre de chaves, que controla o plano de toodata de acesso. Portanto, é recomendável controlar tootightly 'Colaborador' acesso tooyour cofres chave tooensure somente pessoas autorizadas podem acessar e gerenciar sua chave cofres, chaves, segredos e certificados.
> 
> 

## <a name="data-plane-access-control"></a>Controle de acesso do plano de dados
plano de dados do Cofre de chaves Olá consiste em operações que afetam Olá objetos em um cofre de chaves, como certificados, chaves e segredos.  Isso inclui operações-chave, como criar, importar, atualizar, listar, fazer backup de chaves e restaurá-las, operações criptográficas como entrar, verificar, criptografar, descriptografar, encapsular e desencapsular e definir marcas e outros atributos para chaves. Da mesma forma, para segredos, isso inclui obter, definir, listar e excluir.

O acesso do dados do plano é concedido definindo políticas de acesso para um cofre de chaves. Um usuário, grupo ou um aplicativo deve ter permissões de Colaborador (RBAC) para o plano de gerenciamento um cofre de chaves toobe tooset capaz de políticas de acesso para esse Cofre de chaves. Um usuário, grupo ou aplicativo pode ser concedido operações específicas do tooperform de acesso para segredos em um cofre de chaves ou chaves. Suporte de Cofre de chaves too16 entradas de política de acesso para um cofre de chaves. Criar um grupo de segurança do Active Directory do Azure e adicionar usuários toothat grupo toogrant dados plano acesso tooseveral usuários tooa Cofre de chaves.

### <a name="key-vault-access-policies"></a>Políticas de Acesso do cofre de chaves
Políticas de acesso do Cofre de chaves concederem certificados, os segredos e permissões tookeys separadamente. Por exemplo, você pode fornecer uma chave de tooonly de acesso do usuário, mas nenhuma permissão para segredos. No entanto, as chaves de tooaccess de permissões ou segredos ou certificados estão no nível de Cofre de saudação. Em outras palavras, a política de acesso de cofre de chaves não dá suporte a permissões em nível de objeto. Você pode usar [portal do Azure](https://portal.azure.com/), Olá [ferramentas CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [Cofre de chaves APIs REST de gerenciamento](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset as políticas de acesso para um cofre de chaves.

> [!IMPORTANT]
> Observe que as políticas de acesso do Cofre de chaves se aplicam no nível do cofre hello. Por exemplo, quando um usuário é concedido permissão toocreate e excluir as chaves, ela pode executar essas operações em todas as chaves no cofre de chaves.
> 
> 

## <a name="example"></a>Exemplo
Digamos que você esteja desenvolvendo um aplicativo que usa um certificado para SSL, o armazenamento do Azure para armazenar dados e uma chave RSA de 2048 bits para operações de entrada. Digamos que esse aplicativo seja executado em uma VM (ou um Conjunto de Dimensionamento de VM). Você pode usar um toostore de Cofre de chaves que Olá a todos os segredos do aplicativo e use Cofre de chaves toostore Olá bootstrap certificado que é usado pelo Olá tooauthenticate de aplicativo com o Active Directory do Azure.

Portanto, aqui está um resumo de toobe todos os para o chaves e segredos do hello, armazenados em um cofre de chaves.

* **Certificado SSL** - usado para SSL
* **Chave de armazenamento** -usado tooget acesso tooStorage conta
* **Chave de 2048 bits RSA** - usada para operações de entrada
* **Certificado Bootstrap** -usado tooauthenticate tooAzure do Active Directory, chave de armazenamento tooget acesso tookey cofre toofetch hello e chave RSA Olá use para assinatura.

Agora vamos atender às pessoas Olá gerenciar, implantar e auditoria deste aplicativo. Vamos usar três funções neste exemplo.

* **Equipe de segurança** - esses são normalmente a equipe de TI de saudação 'temporária de saudação CSO (diretor de segurança)' ou equivalente, é responsável por Olá proteção adequada de segredos, como SSL certificados, chaves RSA usadas para assinar, cadeias de caracteres de conexão para bancos de dados, chaves de conta de armazenamento.
* **Os desenvolvedores/operadores** -esses são Olá quem desenvolve esse aplicativo e, em seguida, implantá-lo no Azure. Normalmente, eles não fazem parte da equipe de segurança Olá e, portanto, não deveriam acessar tooany os dados confidenciais, como certificados SSL, chaves RSA, mas aplicativo hello implantação deve ter acesso toothose.
* **Auditores** -isso geralmente é um conjunto diferente de pessoas, a isoladas geral equipe de TI e desenvolvedores de saudação. Sua responsabilidade é uso adequado de tooreview e a manutenção de certificados, chaves, etc. e garantir a conformidade com padrões de segurança de dados. 

Há uma função mais do que está fora do escopo Olá esse aplicativo, mas relevante toobe aqui mencionados, e isso seria assinatura hello (ou grupo de recursos) administrador. Administrador de assinatura define as permissões de acesso inicial para a equipe de segurança hello. Aqui vamos supor que esse administrador de assinatura Olá concedeu acesso toohello equipe tooa recurso grupo de segurança no qual todos os Olá recursos necessários para reside neste aplicativo.

Agora vamos ver as ações que cada função executa no contexto de saudação deste aplicativo.

* **Equipe de segurança**
  * Criar cofres de chaves
  * Ativar o registro em log do cofre de chaves
  * Adicionar chaves/segredos
  * Criar o backup de chaves de recuperação de desastre
  * Definir o acesso de Cofre de chaves política toogrant permissões toousers e aplicativos tooperform operações específicas
  * Distribuir periodicamente chaves/segredos
* **Desenvolvedores/operadores**
  * Obter referências toobootstrap e certificados SSL (as impressões digitais), chave de armazenamento (segredo URI) e chave (URI de chave) da equipe de segurança de assinatura
  * Desenvolver e implantar o aplicativo que acessa chaves e segredos de forma programática
* **Auditores**
  * Revisar uso de logs de uso de chave/segredo adequado tooconfirm e conformidade com padrões de segurança de dados

Agora vamos ver o Cofre de tookey de permissões de acesso são necessários por cada função (e o aplicativo hello) tooperform as tarefas atribuídas. 

| Função de Usuário | Permissões do plano de gerenciamento | Permissões do plano de dados |
| --- | --- | --- |
| Equipe de Segurança |Colaborador do cofre de chaves |Chaves: fazer backup, criar, excluir, obter, importar, listar, restaurar <br> Segredos: todos |
| Desenvolvedores/Operador |Cofre de chaves implantar permissão para que VMs Olá implantarem podem buscar segredos do Cofre de chaves de saudação |Nenhum |
| Auditores |Nenhum |Chaves: lista<br>Segredos: lista |
| Aplicativo |Nenhum |Chaves: assinar<br>Segredos: obter |

> [!NOTE]
> Auditores precisam de permissão de lista de chaves e segredos para que ele podem inspecionar atributos de chaves e segredos que não são emitidos nos logs de saudação, como marcas, datas de ativação e expiração.
> 
> 

Além de Cofre de tookey de permissão, todas as três funções também precisam acessar recursos de tooother. Por exemplo, toobe capaz de toodeploy VMs (ou Web Apps etc.) Os desenvolvedores/operadores também precisará de tipos de recurso de toothose de acesso 'Colaborador'. Auditores precisam de acesso de leitura conta de armazenamento de toohello onde Olá Cofre de chaves logs são armazenados.

Como foco Olá deste artigo está protegendo o Cofre de chaves acesso tooyour, vamos apenas ilustram as partes relevantes do hello pertencente toothis tópico e ignorar os detalhes sobre a implantação de certificados, acessar chaves e segredos programaticamente etc. Esses detalhes já são abrangidos em outro lugar. Implantação de certificados armazenados no cofre de chaves tooVMs é abordado em um [postagem de blog](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)e não há [código de exemplo](https://www.microsoft.com/download/details.aspx?id=45343) disponíveis que ilustra como toouse bootstrap certificado tooauthenticate tooAzure AD tooget Cofre de tookey de acesso.

A maioria das permissões de acesso de saudação pode ser concedida usando o portal do Azure, mas permissões granulares toogrant, talvez seja necessário toouse Olá de tooachieve PowerShell do Azure (ou a CLI do Azure) desejado de resultados. 

Suponha Olá trechos de código do PowerShell a seguir:

* administrador do Active Directory do Azure Olá tiver criado grupos de segurança que representam Olá três funções, ou seja, equipe de segurança da Contoso, Devops de aplicativo da Contoso, a Contoso App Auditors. administrador de saudação também adicionou usuários toohello grupos pertencem.
* **ContosoAppRG** é o grupo de recursos de saudação onde residem todos os recursos de saudação. **contosologstorage** é onde os logs de saudação são armazenados. 
* Cofre de chaves **ContosoKeyVault** e conta de armazenamento usado para logs de Cofre de chaves **contosologstorage** deve estar no hello mesmo local do Azure

Primeiro administrador de assinatura Olá atribui Colaborador do Cofre de chave e a equipe de segurança de toohello de funções de ' Administrador de acesso do usuário '. Isso permite que os recursos de tooother Olá segurança team toomanage acesso e gerencie cofres chave no grupo de recursos de saudação ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Olá script a seguir ilustra como equipe de segurança de saudação pode criar um cofre de chaves, o log de instalação e definir permissões de acesso de outras funções e o aplicativo hello. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

função personalizada Olá definido, é só pode ser atribuído toohello assinatura onde o grupo de recursos do hello ContosoAppRG é criado. Se hello mesmo funções personalizadas serão usadas para outros projetos em outras assinaturas, seu escopo poderia ter assinaturas mais adicionadas.

atribuição de função personalizada Olá Olá desenvolvedores/operadores para permissão de "implantar/ação" hello é o grupo de recursos toohello no escopo. Dessa forma apenas as VMs de saudação criado no grupo de recursos de saudação 'ContosoAppRG' obterá segredos hello (certificado SSL e certificados de inicialização). Todas as máquinas virtuais que um membro da equipe de desenvolvimento/ops cria em outro grupo de recursos não será capaz de tooget desses segredos mesmo se sabiam segredo Olá URIs.

Este exemplo ilustra um cenário simples. Cenários do mundo real podem ser mais complexos e talvez seja necessário tooadjust permissões tooyour Cofre de chaves com base em suas necessidades. Por exemplo, em nosso exemplo, vamos supor que equipe de segurança fornecerá chave hello e referências de segredo (URIs e impressões digitais) tooreference de necessidade de equipe que os desenvolvedores/operadores em seus aplicativos. Portanto, não precisam toogrant desenvolvedores/operadores qualquer acesso a dados do plano. Além disso, observe que esse exemplo enfoca a proteção do cofre de chaves. Semelhante deve ser considerado toosecure [suas VMs](https://azure.microsoft.com/services/virtual-machines/security/), [contas de armazenamento](../storage/common/storage-security-guide.md) e outros recursos do Azure muito.

> [!NOTE]
> Observação: esse exemplo mostra como o acesso ao chave de cofres será bloqueado na produção. os desenvolvedores de saudação devem ter seu próprio assinatura ou grupo de recursos onde têm permissões completas toomanage seus cofres, VMs e conta de armazenamento onde eles desenvolverem o aplicativo hello.
> 
> 

## <a name="resources"></a>Recursos
* [Controle de acesso baseado em função do Active Directory do Azure](../active-directory/role-based-access-control-configure.md)
  
  Este artigo explica hello controle de acesso baseado em função do Active Directory do Azure e como ele funciona.
* [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md)
  
  Este artigo detalha todos Olá funções internas disponíveis no RBAC.
* [Noções básicas sobre a implantação do Gerenciador de Recursos e a implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md)
  
  Este artigo explica a implantação do Gerenciador de recursos de saudação e modelos de implantação clássico e explica os benefícios de saudação do uso de grupos de recursos e o Gerenciador de recursos de saudação
* [Gerenciar o Controle de Acesso baseado em função com o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Este artigo explica como o controle com o Azure PowerShell de acesso toomanage baseada em função
* [Gerenciando o controle de acesso baseado em função com hello API REST](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Este artigo mostra como toouse Olá toomanage da API REST RBAC.
* [Role-Based Access Control for Microsoft Azure from Ignite (Controle de Acesso Baseado em Função do Microsoft Azure do Ignite)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Este é um vídeo no Channel 9 da conferência de Ignite 2015 MS Olá de tooa de link. Nessa sessão, falar sobre o acesso a recursos de gerenciamento e geração de relatórios no Azure e explorar as práticas recomendadas para proteger o acesso tooAzure assinaturas usando o Active Directory do Azure.
* [Autorizar o acesso tooweb aplicativos usando OAuth 2.0 e o Active Directory do Azure](../active-directory/active-directory-protocols-oauth-code.md)
  
  Este artigo descreve o fluxo completo do OAuth 2.0 para autenticação com o Azure Active Directory.
* [APIs REST de Gerenciamento de cofre de chaves](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Este documento é referência Olá Olá APIs REST toomanage sua chave de cofre programaticamente, incluindo a definição de política de acesso do Cofre de chaves.
* [APIs REST do cofre de chaves](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Cofre de tookey link documentação de referência da API REST.
* [Controle de acesso a chave](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Vincular tooSecret documentação de referência de controle de acesso.
* [Controle de acesso a segredo](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Vincular tooKey documentação de referência de controle de acesso.
* [Definir](https://msdn.microsoft.com/library/mt603625.aspx) e [Remover](https://msdn.microsoft.com/library/mt619427.aspx) política de acesso do cofre de chaves usando o PowerShell
  
  Documentação de tooreference links de política de acesso do PowerShell cmdlets toomanage Cofre de chaves.

## <a name="next-steps"></a>Próximas etapas
Para ver um tutorial de introdução para um administrador, confira [Introdução ao cofre de chaves do Azure](key-vault-get-started.md).

Para saber mais sobre o log de uso do cofre de chaves, confira [Log do cofre de chaves do Azure](key-vault-logging.md).

Para saber mais sobre o uso de chaves e segredos com o cofre de chaves do Azure, confira [Sobre Chaves e Segredos](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Se você tiver dúvidas sobre o Cofre de chaves, visite Olá [Cofre de chaves do Azure fóruns](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

