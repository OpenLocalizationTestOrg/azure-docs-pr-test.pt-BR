---
title: "Guia de segurança do armazenamento aaaAzure | Microsoft Docs"
description: "Detalhes Olá muitos métodos de proteção de armazenamento do Azure, incluindo, mas não limitado tooRBAC, criptografia do serviço de armazenamento, criptografia do lado do cliente, SMB 3.0 e criptografia de disco do Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Guia de segurança do Armazenamento do Azure
## <a name="overview"></a>Visão geral
Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança que juntos permitem que os desenvolvedores de aplicativos seguros toobuild. conta de armazenamento Olá em si pode ser protegida usando o controle de acesso baseado em função e o Active Directory do Azure. Os dados podem ser protegidos em trânsito, entre um aplicativo e o Azure usando a [Criptografia do cliente](storage-client-side-encryption.md), HTTPS ou SMB 3.0. Dados podem ser definidos toobe criptografado automaticamente quando escritos usando o armazenamento tooAzure [criptografia de serviço de armazenamento (SSE)](storage-service-encryption.md). Sistema operacional e discos de dados usados por máquinas virtuais podem ser definidos toobe criptografada usando [criptografia de disco do Azure](../security/azure-security-disk-encryption.md). Acesso delegado toohello objetos de dados no armazenamento do Azure podem ser concedidos usando [assinaturas de acesso compartilhado](storage-dotnet-shared-access-signature-part-1.md).

Este artigo apresentará uma visão geral de cada um desses recursos de segurança que podem ser usados com o Armazenamento do Azure. São fornecidos links tooarticles que fornecerá detalhes de cada recurso; portanto, você pode facilmente mais investigação em cada tópico.

Aqui estão Olá tópicos toobe abordada neste artigo:

* [Segurança do plano de gerenciamento](#management-plane-security) – proteção da conta de armazenamento

  plano de gerenciamento de saudação consiste Olá recursos usados toomanage sua conta de armazenamento. Nesta seção, falaremos sobre o modelo de implantação do Azure Resource Manager hello e como toocontrol de controle de acesso baseado em função (RBAC) toouse acessar tooyour contas de armazenamento. Também falaremos sobre como gerenciar as chaves de conta de armazenamento e como tooregenerate-los.
* [Segurança de dados do plano](#data-plane-security) – tooYour de acesso de proteção de dados

  Nesta seção, vamos examinar permitir acesso a objetos de dados reais de toohello na sua conta de armazenamento, como arquivos, blobs, filas e tabelas, usando assinaturas de acesso compartilhado e políticas de acesso armazenado. Vamos abordar a SAS de nível de serviço e de nível de conta. Também veremos como toolimit acessar tooa endereço IP específico (ou intervalo de endereços IP), como o protocolo de saudação toolimit usado tooHTTPS e toorevoke uma assinatura de acesso compartilhado, sem esperar que ele tooexpire.
* [Criptografia em trânsito](#encryption-in-transit)

  Esta seção discute como toosecure dados ao transferir para dentro ou fora do armazenamento do Azure. Falaremos sobre Olá recomendado o uso de criptografia de HTTPS e hello usado pelo SMB 3.0 para compartilhamentos de arquivos do Azure. Também, obtemos uma olhada na criptografia do lado do cliente, o que permite que você tooencrypt Olá dados antes que sejam transferidos para o armazenamento em um aplicativo cliente e dados de saudação toodecrypt depois que ela é transferida do armazenamento.
* [Criptografia em repouso](#encryption-at-rest)

  Falaremos sobre criptografia de serviço de armazenamento (SSE), e como você pode habilitá-la para uma conta de armazenamento, resultando em seus blobs de bloco, blobs de página e acrescentar blobs sejam criptografados automaticamente quando gravados tooAzure armazenamento. Podemos também examinar como você pode usar a criptografia de disco do Azure e explorar diferenças básicas hello e casos de criptografia de disco versus SSE versus criptografia do lado do cliente. Examinaremos rapidamente a compatibilidade de FIPS com os computadores do governo norte-americano.
* Usando [Storage Analytics](#storage-analytics) tooaudit acesso do armazenamento do Azure

  Esta seção discute como informações de toofind na análise do armazenamento Olá logs para uma solicitação. Vamos dar uma olhada em análise de armazenamento real de dados de log e ver como toodiscern se uma solicitação é feita com hello armazenamento de chave, com uma assinatura de acesso compartilhado, de conta ou anônima e se ela teve êxito ou falhou.
* [Habilitando clientes com base no navegador usando CORS](#Cross-Origin-Resource-Sharing-CORS)

  Esta seção fala sobre como tooallow recursos de origens cruzadas compartilhando (CORS). Falaremos sobre o acesso entre domínios e como toohandle com recursos CORS Olá criado no armazenamento do Azure.

## <a name="management-plane-security"></a>Segurança do plano de gerenciamento
plano de gerenciamento de saudação consiste em operações que afetam a própria conta de armazenamento hello. Por exemplo, você pode criar ou excluir uma conta de armazenamento, obter uma lista de contas de armazenamento em uma assinatura, recuperar chaves de conta de armazenamento hello ou regenerar chaves de conta de armazenamento hello.

Ao criar uma nova conta de armazenamento, você seleciona um modelo de implantação: Clássico ou Resource Manager. modelo clássico de saudação de criação de recursos no Azure permite apenas a assinatura de toohello acesso tudo ou nada e hello, por sua vez, a conta de armazenamento.

Este guia se concentra no modelo do Gerenciador de recursos de saudação que é hello recomendado significa para a criação de contas de armazenamento. Com contas de armazenamento do Gerenciador de recursos de hello, em vez de assinatura inteira do fornecendo acesso toohello, você pode controlar o acesso em um plano de gerenciamento de nível toohello mais finito usando controle de acesso baseado em função (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Como toosecure sua conta de armazenamento com controle de acesso baseado em função (RBAC)
Vamos falar sobre o que é o RBAC e como você pode usá-lo. Cada assinatura do Azure tem um Azure Active Directory. Usuários, grupos e aplicativos de diretório podem ser concedidos acessar toomanage recursos em Olá assinatura do Azure que usam o modelo de implantação do Gerenciador de recursos de saudação. Isso é chamado tooas controle de acesso baseado em função (RBAC). toomanage acessar, você pode usar o hello [portal do Azure](https://portal.azure.com/), Olá [ferramentas CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [APIs de REST do provedor de recursos de armazenamento do Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Com o modelo do Gerenciador de recursos de hello, coloque o conta de armazenamento Olá em um recurso grupo e controle de acesso toohello plano de gerenciamento de conta de armazenamento específico usando o Azure Active Directory. Por exemplo, você pode conceder a usuários específicos Olá capacidade tooaccess Olá chaves conta de armazenamento, enquanto outros usuários podem exibir informações sobre a conta de armazenamento hello, mas não é possível acessar chaves de conta de armazenamento hello.

#### <a name="granting-access"></a>Concessão de acesso
Acesso atribuindo Olá apropriado RBAC função toousers, grupos e aplicativos, no escopo de saudação à direita. assinatura inteira do toogrant acesso toohello, você atribui uma função no nível de assinatura de saudação. Você pode conceder acesso tooall de recursos de saudação em um grupo de recursos, concedendo permissões toohello recurso próprio grupo. Você também pode atribuir funções específicas toospecific recursos, como contas de armazenamento.

Aqui estão as principais pontos de saudação que você precisa tooknow sobre como usar o RBAC tooaccess Olá as operações de gerenciamento de uma conta de armazenamento do Azure:

* Quando você atribuir acesso, você basicamente atribuir uma conta de toohello de função que você deseja acesso toohave. Você pode controlar o acesso toohello operações usadas toomanage essa conta de armazenamento, mas não os dados toohello objetos na conta de saudação. Por exemplo, você pode conceder permissão tooretrieve propriedades de saudação da conta de armazenamento de saudação (por exemplo, redundância), mas não o contêiner tooa ou dados dentro de um contêiner no armazenamento de Blob.
* Alguém toohave permissão tooaccess Olá objetos de dados na conta de armazenamento hello, pode dar a eles chaves de conta de armazenamento permissão tooread hello e que o usuário pode usar essas chaves tooaccess Olá blobs, filas, tabelas e arquivos.
* Funções podem ser atribuídas tooa conta de usuário específica, um grupo de usuários ou aplicativos específicos tooa.
* Cada função tem uma lista de Ações e de Não Ações. Por exemplo, a função de Colaborador de máquina Virtual de saudação tem uma ação do listkeys "do" que permite ler Olá toobe de chaves de conta de armazenamento. Olá colaborador tem "Não ações" como atualizar o acesso de saudação para usuários de saudação do Active Directory.
* Funções de armazenamento incluem (mas não estão limitadas a) a seguir hello:

  * Proprietário – ele pode gerenciar tudo, inclusive o acesso.
  * Colaborador – eles podem fazer qualquer coisa proprietário Olá possa ser atribuir acesso. Alguém com essa função pode exibir e regenerar chaves de conta de armazenamento de saudação. Com chaves de conta de armazenamento hello, eles podem acessar os objetos de dados de saudação.
  * Leitor – eles podem exibir informações sobre a conta de armazenamento hello, exceto os segredos. Por exemplo, se você atribuir uma função com permissões de leitura de saudação toosomeone de conta de armazenamento, podem exibir propriedades Olá Olá da conta de armazenamento, mas eles não podem fazer alterações de propriedades toohello ou exibir chaves de conta de armazenamento hello.
  * Colaborador da conta de armazenamento – podem gerenciar conta de armazenamento hello – eles podem ler Olá da assinatura grupos de recursos e recursos e criar e gerenciar implantações de grupos de recursos de assinatura. Eles também podem acessar as chaves de conta de armazenamento hello, que por sua vez, significa que eles possam acessar o plano de dados de saudação.
  * Administrador de acesso do usuário – eles podem gerenciar conta de armazenamento de toohello de acesso do usuário. Por exemplo, eles podem conceder usuário específico do leitor acesso tooa.
  * Colaborador da máquina virtual – podem gerenciar máquinas virtuais, mas não Olá armazenamento conta toowhich que estão conectados. Essa função pode listar chaves de conta de armazenamento hello, que significa que Olá toowhom de usuário que você atribuir essa função pode atualizar o plano de dados hello.

    Para um usuário de toocreate uma máquina virtual, é que toobe toocreate capaz de saudação correspondente arquivo VHD em uma conta de armazenamento. toodo, necessidade de armazenamento de saudação do toobe tooretrieve capaz de chave de conta e passá-lo API toohello criando Olá VM. Portanto, eles devem ter essa permissão para eles podem listar chaves de conta de armazenamento hello.
* funções personalizadas do Hello capacidade toodefine é um recurso que permite que você toocompose um conjunto de ações de uma lista de ações disponíveis que podem ser executadas em recursos do Azure.
* usuário Olá tem toobe configurado no Active Directory do Azure antes de atribuir uma função toothem.
* Você pode criar um relatório do que concedido/revogado que tipo de acesso de quem e o escopo usando o PowerShell ou Olá CLI do Azure.

#### <a name="resources"></a>Recursos
* [Controle de acesso baseado em função do Active Directory do Azure](../active-directory/role-based-access-control-configure.md)

  Este artigo explica hello controle de acesso baseado em função do Active Directory do Azure e como ele funciona.
* [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md)

  Este artigo fornece detalhes sobre todas as funções internas do hello disponíveis no RBAC de.
* [Noções básicas sobre a implantação do Gerenciador de Recursos e a implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md)

  Este artigo explica a implantação do Gerenciador de recursos de saudação e modelos de implantação clássico e explica os benefícios de saudação do uso de grupos de recursos e o Gerenciador de recursos de saudação. Ele explica como provedores de armazenamento, rede e saudação de computação do Azure funcionam no modelo do Gerenciador de recursos de saudação.
* [Gerenciando o controle de acesso baseado em função com hello API REST](../active-directory/role-based-access-control-manage-access-rest.md)

  Este artigo mostra como toouse Olá toomanage da API REST RBAC.
* [Azure Storage Resource Provider REST API Reference (Referência à API REST do provedor de recursos de armazenamento do Azure)](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Esta é a referência Olá para Olá APIs que você pode usar toomanage sua conta de armazenamento programaticamente.
* [Tooauth do guia do desenvolvedor com a API do Gerenciador de recursos do Azure](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Este artigo mostra como usar tooauthenticate Olá APIs do Gerenciador de recursos.
* [Role-Based Access Control for Microsoft Azure from Ignite (Controle de Acesso Baseado em Função do Microsoft Azure do Ignite)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Este é um vídeo no Channel 9 da conferência de Ignite 2015 MS Olá de tooa de link. Nessa sessão, falar sobre o acesso a recursos de gerenciamento e geração de relatórios no Azure e explorar as práticas recomendadas para proteger o acesso tooAzure assinaturas usando o Active Directory do Azure.

### <a name="managing-your-storage-account-keys"></a>Gerenciando as chaves da conta de armazenamento
Conta de armazenamento chaves são cadeias de 512 bits criadas pelo Azure que, juntamente com o armazenamento de saudação, o nome da conta pode ser usado tooaccess objetos de dados de Olá armazenados na conta de armazenamento hello, por exemplo, os blobs, as entidades dentro de uma tabela, fila de mensagens e arquivos em um compartilhamento de arquivo do Azure. Controles de chaves de conta de armazenamento do acesso toohello controlar acesso toohello plano de dados para essa conta de armazenamento.

Cada conta de armazenamento tem duas chaves chamadas tooas "Chave 1" e "Chave 2" no hello [portal do Azure](http://portal.azure.com/) e em Olá cmdlets do PowerShell. Eles podem ser regenerados manualmente usando um dos vários métodos, incluindo, mas não limitado toousing Olá [portal do Azure](https://portal.azure.com/), Olá biblioteca de cliente de armazenamento do .NET ou hello Azure PowerShell, Olá CLI do Azure ou programaticamente usando API REST de serviços de armazenamento.

Há inúmeros motivos tooregenerate suas chaves de conta de armazenamento.

* Você pode regenerá-las regularmente por motivos de segurança.
* Você poderia regenerar suas chaves de conta de armazenamento se alguém gerenciados toohack em um aplicativo e recuperar a chave de saudação que foi codificado ou salvo em um arquivo de configuração, oferecendo a eles a conta de armazenamento tooyour acesso completo.
* Outro caso de regeneração da chave é se sua equipe estiver usando um aplicativo do Gerenciador de armazenamento que retém a chave de conta de armazenamento Olá, e um dos membros da equipe Olá deixa. aplicativo Hello continuaria toowork, oferecendo a eles acesso tooyour armazenamento conta depois que eles são excluídos. Isso é realmente Olá motivo principal criaram assinaturas de acesso compartilhado do nível de conta – você pode usar um SAS de nível de conta em vez de armazenar as chaves de acesso de saudação em um arquivo de configuração.

#### <a name="key-regeneration-plan"></a>Plano de nova geração de chave
Você não quer chave de regenerar Olá toojust que você estiver usando sem um planejamento. Se você fizer isso, você poderia cortado todos acesso toothat conta de armazenamento, que pode causar a interrupção principal. É por isso que há duas chaves. Você deve regenerar uma chave de cada vez.

Antes de você regenera suas chaves, certifique-se de que você tem uma lista de todos os aplicativos que dependem da conta de armazenamento hello, bem como qualquer outro serviço que você está usando no Azure. Por exemplo, se você estiver usando serviços de mídia do Azure que dependem de sua conta de armazenamento, você deverá ressincronizar as chaves de acesso de saudação com o serviço de mídia após você regenerar a chave de saudação. Se você estiver usando qualquer aplicativo, como um Gerenciador de armazenamento, você precisará tooprovide Olá novas chaves toothose aplicativos também. Observe que se você tiver VMs cujos arquivos VHD são armazenados na conta de armazenamento hello, eles não serão afetados pela regeneração de chaves de conta de armazenamento hello.

Você pode gerar novamente as chaves no portal do Azure de saudação. Depois que as chaves são geradas novamente podem ocupar too10 toobe minutos sincronizados em todos os serviços de armazenamento.

Quando estiver pronto, aqui está o processo geral de saudação detalhando como você deve alterar sua chave. Nesse caso, Olá pressupõe-se que você está usando chaves 1 e for toochange tudo toouse chave 2 em vez disso.

1. Regenere chave 2 tooensure que ele é seguro. Você pode fazer isso no hello portal do Azure.
2. Em todos os aplicativos de saudação onde a chave de armazenamento de saudação é armazenada, altere o valor de novo de Olá armazenamento toouse chave chave 2. Testar e publicar o aplicativo hello.
3. Depois que todos os de saudação aplicativos e serviços estão ativos e em execução com êxito, regenerar a chave 1. Isso garante que qualquer pessoa toowhom não têm expressamente nova chave de saudação não terá mais acesso toohello conta de armazenamento.

Se você estiver usando 2 de chave, você pode usar o hello mesmo processo, mas os nomes de chave Olá inversa.

Você pode migrar em dois dias, alterando a nova chave cada aplicativo toouse hello e publicá-la. Depois que todos eles, você deve, em seguida, volte e regenerar chave antiga Olá para que ele não funciona mais.

Outra opção é a chave da conta de armazenamento tooput Olá em um [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) como um segredo e ter sua chave de saudação recuperar aplicativos a partir daí. Em seguida, quando você regenerar a chave hello e atualizar Olá Cofre de chaves do Azure, aplicativos de saudação não serão necessário toobe reimplantado porque eles assumirão a nova chave de saudação do hello Azure Key Vault automaticamente. Observe que você pode fazer com que o aplicativo hello ler a chave de saudação cada vez que você precisar, ou você pode armazenar em cache na memória e se ele falhar quando usá-lo, recuperar a chave de saudação novamente do hello Azure Key Vault.

Usar o Cofre de Chaves do Azure também acrescenta outro nível de segurança para suas chaves de armazenamento. Se você usar esse método, você nunca terá que Olá armazenamento chave codificado em um arquivo de configuração, que remove essa via de alguém obtendo toohello chaves sem permissão de acesso.

Outra vantagem de usar o Cofre de chaves do Azure é que você também pode controlar o acesso tooyour chaves usando o Active Directory do Azure. Isso significa que você pode conceder a série de toohello de acesso de aplicativos que precisam tooretrieve chaves de saudação do Cofre de chaves do Azure e saber que outros aplicativos não será capaz de tooaccess chaves de saudação sem conceder permissão especificamente.

Observação: é recomendável toouse somente uma saudação chaves em todos os aplicativos em Olá mesmo tempo. Se você usar a chave em alguns locais keys 1 e 2 em outros, você não poderá ser capaz de toorotate suas chaves sem algum aplicativo perder o acesso.

#### <a name="resources"></a>Recursos
* [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md#regenerate-storage-access-keys)

  Esse artigo fornece uma visão geral das contas de armazenamento e aborda a exibição, a cópia e a regeneração das chaves de acesso de armazenamento.
* [Azure Storage Resource Provider REST API Reference (Referência à API REST do provedor de recursos de armazenamento do Azure)](https://msdn.microsoft.com/library/mt163683.aspx)

  Este artigo contém artigos de toospecific links sobre chaves de conta de armazenamento de recuperação hello e chaves de conta de armazenamento Olá Regenerando para uma conta do Azure usando a API REST de saudação. Observação: isto é para as contas de armazenamento do Resource Manager.
* [Operations on storage accounts (Operações nas contas de armazenamento)](https://msdn.microsoft.com/library/ee460790.aspx)

  Este artigo na Olá Reference da API REST Gerenciador de serviço de armazenamento contém artigos de toospecific de links na recuperação e regenerar chaves de conta de armazenamento hello usando Olá API REST. Observação: Esta é a saudação clássico para contas de armazenamento.
* [Digamos que o gerenciamento de tookey adeus – gerenciar acesso tooAzure armazenamento dados usando o Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Este artigo mostra como toouse do Active Directory toocontrol acesso a chaves de armazenamento do Azure tooyour no cofre de chaves do Azure. Ele também mostra como chaves de saudação tooregenerate por hora do trabalho toouse um objeto de automação do Azure.

## <a name="data-plane-security"></a>Segurança do plano de dados
Segurança de plano de dados refere-se métodos toohello os objetos de dados de saudação toosecure usado armazenados no armazenamento do Azure – arquivos, filas, tabelas e blobs hello. Já vimos métodos tooencrypt Olá dados e segurança durante o trânsito de dados hello, mas como você efetuará permitindo acesso toohello objetos?

Basicamente, há dois métodos para controlar acesso toohello dados próprios objetos. Olá é primeiro por controlar chaves de conta de armazenamento para toohello acesso e Olá segundo é usar assinaturas de acesso compartilhado toogrant acesso toospecific dados objetos para um determinado período de tempo.

Um toonote de exceção é que você pode permitir acesso público tooyour blobs definindo o nível de acesso de saudação de contêiner Olá que contém blobs Olá adequadamente. Se você definir o acesso para um contêiner tooBlob ou contêiner, isso permitirá o acesso de leitura público para blobs Olá nesse contêiner. Isso significa que qualquer pessoa com uma URL apontando tooa blob nesse contêiner poderá abri-lo em um navegador sem usar uma assinatura de acesso compartilhado ou ter chaves de conta de armazenamento hello.

### <a name="storage-account-keys"></a>Chaves da conta de armazenamento
Chaves da conta de armazenamento são cadeias de caracteres de 512 bits criadas pelo Azure que, juntamente com o nome de conta de armazenamento Olá, pode ser objetos de dados de saudação de tooaccess usado armazenados na conta de armazenamento hello.

Por exemplo, você pode ler blobs, escrever tooqueues, criar tabelas e modificar arquivos. Muitas dessas ações podem ser executadas por meio de hello Azure portal, ou usando um dos muitos aplicativos do Gerenciador de armazenamento. Você também pode escrever código toouse de saudação API REST ou uma saudação bibliotecas de cliente de armazenamento tooperform essas operações.

Como discutido na seção de saudação em Olá [segurança do plano de gerenciamento](#management-plane-security), acesso toohello chaves de armazenamento para uma conta de armazenamento do clássico pode ser concedida, fornecendo acesso completo toohello assinatura do Azure. Chaves de armazenamento de toohello de acesso para uma conta de armazenamento usando o modelo do Azure Resource Manager Olá podem ser controladas por meio do controle de acesso baseado em função (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Como toodelegate acessar tooobjects em sua conta usando assinaturas de acesso compartilhado e políticas de acesso armazenada
Uma assinatura de acesso compartilhado é uma cadeia de caracteres que contém um token de segurança que pode ser anexado tooa URI que permite que você toodelegate acessar toostorage objetos e especificar restrições, como permissões de saudação e intervalo de data/hora de saudação do access.

Você pode conceder acesso tooblobs, contêineres, fila de mensagens, arquivos e tabelas. Com tabelas, você pode, na verdade, conceder permissão tooaccess um intervalo de entidades na tabela Olá especificando Olá partição e a linha de intervalos de chaves toowhich quiser Olá usuário toohave acesso. Por exemplo, se você tiver dados armazenados com uma chave de partição do estado geográfico, você pode dar a alguém acesso toojust Olá dados para Califórnia.

Em outro exemplo, você pode dar um token SAS que permite que ele toowrite fila de tooa de entradas de um aplicativo da web e fornecer um operador de aplicativo de função mensagens tooget token SAS de saudação da fila e processá-los. Ou você pode dar a um cliente um token SAS pode usar o contêiner de tooa tooupload imagens no armazenamento de Blob e dar um tooread de permissão de aplicativo web essas imagens. Em ambos os casos, há uma separação de preocupações – cada aplicativo pode receber acesso Olá apenas necessário em ordem tooperform sua tarefa. Isso é possível por meio do uso de saudação de assinaturas de acesso compartilhado.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Por que você deseja toouse assinaturas de acesso compartilhado
Por que você queira toouse um SAS em vez de apenas forneça sua chave de conta de armazenamento, que é muito mais fácil? Forneça sua chave de conta de armazenamento é como chaves de saudação do Reino seu armazenamento de compartilhamento. Isto é, ela concede acesso a tudo. Alguém poderia usar as chaves e carregar sua conta de armazenamento inteira de músicas tooyour de biblioteca. Ele também poderia substituir seus arquivos por versões infectadas por vírus ou até mesmo roubar seus dados. Dar conta de armazenamento tooyour acesso ilimitado é algo que não devem ser tomadas pouco.

Com assinaturas de acesso compartilhado, você pode dar a um cliente apenas as permissões de saudação necessárias por uma quantidade limitada de tempo. Por exemplo, se alguém está carregando uma conta de tooyour de blob, você pode conceder a eles acesso de gravação para suficiente blob de saudação do tempo tooupload (dependendo do tamanho de saudação do blob Olá, é claro). E se você mudar de ideia, poderá revogar esse acesso.

Além disso, você pode especificar que solicitações feitas usando uma SAS restrita tooa determinado tooAzure externo do intervalo de endereços IP ou endereço IP. Você também pode exigir que as solicitações sejam feitas usando um protocolo específico (HTTPS ou HTTP/HTTPS). Isso significa que se deseja apenas o tráfego HTTPS tooallow tooHTTPS de protocolo hello necessária somente podem ser definidas e o tráfego HTTP será bloqueado.

#### <a name="definition-of-a-shared-access-signature"></a>Definição de uma Assinatura de Acesso Compartilhado
Uma assinatura de acesso compartilhado é que um conjunto de parâmetros de consulta acrescentada toohello URL apontando para o recurso de saudação

que fornece informações sobre o acesso de saudação permitido e Olá período de tempo para o qual Olá acesso é permitido. Aqui está um exemplo. esse URI fornece acesso de leitura tooa blob para cinco minutos. Observe que os parâmetros de consulta SAS devem ser Codificados pela URL, como %3A para dois-pontos (:) e %20 para um espaço.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Como Olá assinatura de acesso compartilhado é autenticada pelo Olá serviço de armazenamento do Azure
Quando o serviço de armazenamento Olá recebe a solicitação de hello, ele usa parâmetros de consulta de entrada hello e cria uma assinatura usando Olá mesmo método como Olá programa de chamada. Em seguida, compara duas assinaturas de saudação. Se concordar, então Olá serviço de armazenamento pode verificar Olá storage service versão toomake se que ele é válido, verificar se hello data e hora atuais estão dentro da janela especificada hello, certifique-se de acesso de Olá solicitado corresponde toohello solicitação feita, etc.

Por exemplo, com nosso URL acima, se Olá URL foi apontando tooa arquivo em vez de um blob, esta solicitação falhará porque ela especifica que Olá que assinatura de acesso compartilhado é para um blob. Se Olá comando REST que está sendo chamado tooupdate um blob, falharia porque hello assinatura de acesso compartilhado Especifica que somente o acesso de leitura é permitido.

#### <a name="types-of-shared-access-signatures"></a>Tipos de Assinatura de Acesso Compartilhado
* Uma SAS de nível de serviço pode ser usado tooaccess a recursos específicos em uma conta de armazenamento. Alguns exemplos são recuperando uma lista de blobs em um contêiner, baixar um blob, atualizar uma entidade em uma tabela, adicionando a fila de mensagens de tooa ou carregando um compartilhamento de arquivos do arquivo tooa.
* Uma SAS de nível de conta pode ser usado tooaccess qualquer coisa que uma SAS de nível de serviço pode ser usada para. Além disso, ela pode fornecer tooresources opções que não são permitidas com uma SAS de nível de serviço, como contêineres de toocreate capacidade hello, tabelas, filas e compartilhamentos de arquivos. Você também pode especificar os serviços de acesso toomultiple ao mesmo tempo. Por exemplo, você pode dar a alguém acessar tooboth blobs e os arquivos na sua conta de armazenamento.

#### <a name="creating-an-sas-uri"></a>Criação de um URI de SAS
1. Você pode criar um URI ad-hoc sob demanda, definindo todos os parâmetros de consulta de saudação de cada vez.

   Isso é realmente flexível, mas se você tiver um conjunto lógico de parâmetros que sempre são semelhantes, usar uma Política de Acesso Armazenado é uma opção mais adequada.
2. É possível criar uma Política de Acesso Armazenado para um contêiner inteiro, um compartilhamento de arquivos, uma tabela ou uma fila. Em seguida, você pode usar isso como base Olá para Olá URIs de SAS que você criar. As permissões com base em Políticas de Acesso Armazenado podem ser facilmente revogadas. Você pode ter até too5 políticas definidas em cada contêiner, fila, tabela ou compartilhamento de arquivos.

   Por exemplo, se você fosse toohave muitas pessoas leem blobs Olá em um contêiner específico, você pode criar uma política de acesso armazenada que diz "conceder acesso de leitura" e outras configurações que serão Olá mesmo cada vez. Em seguida, você pode criar um URI de SAS usando configurações de saudação do hello política de acesso armazenado e especificando a data/hora de expiração de saudação. Olá vantagem disso é que você não tem toospecify todos Olá parâmetros de consulta cada vez.

#### <a name="revocation"></a>Revogação
Suponha que seu SAS tiver sido comprometida ou deseja toochange-lo devido a requisitos de conformidade normativa ou de segurança corporativa. Como você deseja revogar acesso tooa recurso usando esse SAS? Ele depende de como você criou Olá URI SAS.

Se estiver usando URIs ad hoc, você terá três opções. Você pode emitir tokens SAS com as políticas de expiração curto e simplesmente aguardar Olá SAS tooexpire. Você pode renomear ou excluir o recurso de saudação (supondo que o token Olá foi tooa escopo único objeto). Você pode alterar as chaves de conta de armazenamento hello. Essa última opção pode ter um grande impacto, dependendo de quantos serviços estão usando a conta de armazenamento e provavelmente não é algo que deseja toodo sem um planejamento.

Se você estiver usando uma SAS derivada de uma política de acesso armazenada, você pode remover o acesso Revogando Olá a política de acesso armazenado – você pode alterá-la apenas para que ele expirou ou você pode removê-lo completamente. Isso entra em vigor imediatamente e invalida cada SAS criada usando essa Política de Acesso Armazenado. Atualizar ou remover Olá política de acesso armazenada pode afetar pessoas acessando esse contêiner específico, compartilhamento de arquivos, tabela ou fila por meio de SAS, mas se hello clientes são gravados para solicitarem uma nova SAS quando Olá antigo se torna inválido, isso funciona bem.

Porque o uso de uma SAS derivada de uma política de acesso armazenado oferece Olá capacidade toorevoke que SAS imediatamente, é Olá recomendado tooalways de prática recomendada usar políticas de acesso armazenado quando possível.

#### <a name="resources"></a>Recursos
Para obter mais informações sobre como usar assinaturas de acesso compartilhado e armazenados políticas de acesso, com exemplos, consulte toohello artigos a seguir:

* Esses são os artigos de referência de saudação.

  * [Service SAS (SAS de serviço)](https://msdn.microsoft.com/library/dn140256.aspx)

    Esse artigo fornece exemplos de como usar uma SAS de nível de serviço com blobs, mensagens da fila, intervalos de tabelas e arquivos.
  * [Constructing a service SAS (Criação de uma SAS de serviço)](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Constructing an account SAS (Criação de uma SAS de conta)](https://msdn.microsoft.com/library/mt584140.aspx)
* Esses são os tutoriais para usar o hello .NET cliente biblioteca toocreate assinaturas de acesso compartilhado e políticas de acesso armazenado.

  * [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md)
  * [Compartilhado assinaturas de acesso, parte 2: Criar e usar uma SAS com hello serviço Blob](storage-dotnet-shared-access-signature-part-2.md)

    Este artigo inclui uma explicação do modelo SAS hello, exemplos de assinaturas de acesso compartilhado, e usam as recomendações de prática recomendada de saudação de SAS. Também é discutido é revogação de saudação de permissão de saudação.
* Limite do acesso por endereço IP (ACLs de IP)

  * [O que é uma ACL (Lista de Controle de Acesso) do ponto de extremidade?](../virtual-network/virtual-networks-acl.md)
  * [Constructing a Service SAS (Criação de uma SAS de serviço)](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Este é o artigo de referência Olá SAS de nível de serviço; Ele inclui um exemplo de atuação de IP.
  * [Constructing an Account SAS (Criação de uma SAS de conta)](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Este é o artigo de referência Olá SAS de nível de conta; Ele inclui um exemplo de atuação de IP.
* Autenticação

  * [Autenticação para Olá serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Tutorial de introdução às Assinaturas de Acesso Compartilhado

  * [SAS Getting Started Tutorial (Tutorial de introdução à SAS)](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Criptografia em trânsito
### <a name="transport-level-encryption--using-https"></a>Criptografia no nível de transporte – usando HTTPS
Outra etapa, você deve executar a segurança de saudação tooensure dos seus dados de armazenamento do Azure é dados de saudação tooencrypt entre cliente hello e armazenamento do Azure. Olá primeiro recomenda tooalways usar Olá [HTTPS](https://en.wikipedia.org/wiki/HTTPS) Olá de protocolo, o que garante uma comunicação segura pela Internet pública.

toohave um canal de comunicação seguro, você sempre deve usar HTTPS ao chamar hello APIs REST ou acessar objetos no armazenamento. Além disso, **assinaturas de acesso compartilhado**, que pode ser usado toodelegate acessar objetos de armazenamento tooAzure, incluem uma opção toospecify que Olá somente pode ser usado o protocolo HTTPS ao usar assinaturas de acesso compartilhado, garantindo que qualquer pessoa envio de links com tokens SAS usará o protocolo apropriado de saudação.

Você pode impor o uso de saudação de HTTPS ao chamar objetos de tooaccess de APIs REST Olá nas contas de armazenamento, permitindo que [necessária de transferência segura](storage-require-secure-transfer.md) Olá conta de armazenamento. As conexões que usam HTTP serão recusadas depois que essa opção for habilitada.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Usar criptografia durante a transferência com Compartilhamentos de Arquivos do Azure
Armazenamento de arquivo do Azure dá suporte a HTTPS ao usar a API REST de saudação, mas é mais comumente usado como um compartilhamento de arquivos SMB anexado tooa VM. SMB 2.1 não oferece suporte a criptografia, portanto conexões só são permitidos no hello mesmo região no Azure. No entanto, SMB 3.0 oferece suporte à criptografia e está disponível no Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, permitindo entre regiões de acesso e até mesmo acesso na área de trabalho de saudação.

Observe que enquanto compartilhamentos de arquivos do Azure podem ser usados com Unix, Olá cliente Linux SMB não ainda dá suporte a criptografia, para que acesso só é permitido dentro de uma região do Azure. Suporte à criptografia para Linux é roteiro de saudação de desenvolvedores do Linux responsáveis pela funcionalidade do SMB. Ao adicionar criptografia, você terá Olá a mesma capacidade para acessar um compartilhamento de arquivos do Azure no Linux, como faria para o Windows.

Você pode impor o uso de saudação da criptografia com hello serviço arquivos do Azure, permitindo [necessária de transferência segura](storage-require-secure-transfer.md) Olá conta de armazenamento. Se usar hello APIs REST, HTTPs é necessário. Para o SMB, apenas as conexões SMB que dão suporte à criptografia se conectarão com êxito.

#### <a name="resources"></a>Recursos
* [Como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md)

  Este artigo mostra como toomount um arquivo do Azure compartilham um arquivos de sistema e upload/download do Linux.
* [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md)

  Este artigo fornece uma visão geral dos compartilhamentos de arquivos do Azure e como toomount e usá-los usando o PowerShell e .NET.
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  Este artigo anuncia a disponibilidade geral de saudação do armazenamento de arquivos do Azure e fornece detalhes técnicos sobre a criptografia de saudação SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Usando dados de toosecure de criptografia do lado do cliente que você envie toostorage
Outra opção que ajuda a garantir que os dados sejam protegidos enquanto estão sendo transferidos entre um aplicativo cliente e o Armazenamento é a Criptografia do Cliente. Olá dados são criptografados antes de serem transferidos para o armazenamento do Azure. Ao recuperar dados de saudação do armazenamento do Azure, os dados de saudação são descriptografados depois de ser recebida no lado do cliente de saudação. Embora dados saudação são criptografados, passando pela transmissão de saudação, é recomendável que você também use HTTPS, pois ela tem verificações de integridade de dados internas que ajuda a reduzir os erros de rede que afetam a integridade Olá dos dados de saudação.

Criptografia do lado do cliente também é um método para criptografar os dados em repouso, como dados de saudação são armazenados em formato criptografado. Falaremos sobre isso mais detalhadamente na seção de saudação em [criptografia em repouso](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Criptografia em repouso
Há três recursos do Azure que fornecem criptografia em repouso. Criptografia de disco do Azure é usado tooencrypt Olá SO e discos de dados em máquinas virtuais. Olá outros dois – criptografia do lado do cliente e SSE – são usados tooencrypt de dados no armazenamento do Azure. Examinaremos cada um deles e, em seguida, faremos uma comparação e veremos quando cada um deles pode ser usado.

Enquanto você pode usar dados de saudação do cliente criptografia tooencrypt em trânsito (que também é armazenado em formato criptografado no armazenamento), você pode preferir toosimply use HTTPS durante a transferência de saudação e ter alguma maneira para Olá dados toobe criptografado automaticamente quando for armazenados. Há dois toodo de maneiras isso – SSE e criptografia de disco do Azure. Uma é usada toodirectly criptografar dados de saudação no sistema operacional e discos de dados usados por máquinas virtuais e Olá outros tooencrypt usada dados gravados tooAzure armazenamento de Blob.

### <a name="storage-service-encryption-sse"></a>SSE (Criptografia do Serviço de Armazenamento)
SSE permite toorequest que o serviço de armazenamento de saudação criptografa automaticamente os dados hello quando escrever tooAzure armazenamento. Ao ler dados de saudação do armazenamento do Azure, ele será descriptografado pelo serviço de armazenamento de saudação antes de serem retornados. Isso permite que você toosecure os dados sem ter que toomodify código ou adicionem código tooany aplicativos.

Essa é uma configuração que se aplica a conta de armazenamento inteira toohello. Você pode habilitar e desabilitar esse recurso alterando Olá valor de configuração de saudação. toodo isso, você pode usar Olá Olá do portal do Azure, o PowerShell, CLI do Azure, Olá API de REST do provedor de recursos de armazenamento ou Olá biblioteca de cliente de armazenamento do .NET. Por padrão, a SSE é desativada.

Neste momento, chaves Olá usadas para criptografia de saudação são gerenciadas pela Microsoft. Podemos gerar chaves Olá originalmente e gerenciar de armazenamento seguro de chaves hello, bem como rotação regular Olá Olá conforme definido pela política interna do Microsoft. Olá futura, você obter Olá capacidade toomanage suas próprias chaves de criptografia e forneça um caminho de migração de chaves gerenciados pelo Microsoft gerenciado toocustomer chaves.

Este recurso está disponível para contas Standard e Premium armazenamento criadas usando o modelo de implantação do Gerenciador de recursos de saudação. SSE aplica-se apenas o tooblock blobs, blobs de página e blobs de acréscimo. Olá outros tipos de dados, incluindo tabelas, filas e arquivos, não serão criptografados.

Dados somente serão criptografados quando SSE está habilitado e dados de saudação são gravados tooBlob armazenamento. Habilitar ou desabilitar a SSE não afeta os dados existentes. Em outras palavras, quando você habilita essa criptografia, ele não voltar e criptografar os dados que já existe; nem descriptografará dados Olá já existente quando você desabilita SSE.

Se você quiser toouse esse recurso com uma conta de armazenamento do clássico, você pode criar uma nova conta de armazenamento do Gerenciador de recursos e use AzCopy toocopy Olá dados toohello nova conta.

### <a name="client-side-encryption"></a>Criptografia do cliente
Mencionamos criptografia do lado do cliente ao abordar Olá criptografia de dados de saudação em trânsito. Esse recurso permite que você tooprogrammatically criptografar os dados em um aplicativo cliente antes de enviá-lo por Olá durante a transmissão toobe gravado tooAzure armazenamento e tooprogrammatically descriptografar os dados após recuperá-lo do armazenamento do Azure.

Isso fornece criptografia em trânsito, mas ele também fornece o recurso de saudação de criptografia em repouso. Observe que embora Olá dados são criptografados em trânsito, ainda é recomendável usando vantagem de tootake HTTPS de verificações de integridade de dados internos Olá que ajudam a reduzir os erros de rede que afetam a integridade Olá dos dados de saudação.

Um exemplo de onde você pode usar isso é se você tiver um aplicativo web que armazena blobs e recupera os blobs, e você quiser aplicativo hello e dados toobe tão seguro quanto possível. Nesse caso, você usa a criptografia do cliente. tráfego de saudação entre cliente hello e hello serviço Blob do Azure contém recursos Olá criptografado e ninguém pode interpretar Olá dados em trânsito e reconstitui-lo em seus blobs privadas.

Criptografia do lado do cliente é criada em Java hello e Olá .NET armazenamento bibliotecas de cliente, que por sua vez, use Olá APIs de Cofre de chave do Azure, facilitando muito fácil para você tooimplement. processo de saudação de criptografar e descriptografar dados saudação usa Olá envelope técnica e armazena os metadados usados pela criptografia de saudação em cada objeto de armazenamento. Por exemplo, para blobs, armazená-lo nos metadados de blob hello, enquanto para filas, ele adiciona tooeach mensagem da fila.

Para criptografia de saudação em si, você pode gerar e gerenciar suas próprias chaves de criptografia. Você também pode usar as chaves geradas pelo Olá biblioteca de cliente de armazenamento do Azure, ou você pode ter hello Azure Key Vault gerar chaves de saudação. É possível armazenar as chaves de criptografia em seu armazenamento de chaves local ou armazená-las no Cofre de Chaves do Azure. Cofre de chaves do Azure permite que você toogrant segredos de toohello de acesso no Azure Key Vault toospecific usuários do Active Directory do Azure. Isso significa que não apenas a qualquer pessoa pode ler hello Azure Key Vault e recuperar chaves Olá que você está usando para criptografia do lado do cliente.

#### <a name="resources"></a>Recursos
* [Criptografar e Descriptografar Blobs no Armazenamento do Microsoft Azure usando o Cofre da Chave do Azure](storage-encrypt-decrypt-blobs-key-vault.md)

  Este artigo mostra como toouse a criptografia do lado do cliente com o Cofre de chaves do Azure, incluindo como toocreate Olá KEK e armazená-la no cofre hello usando o PowerShell.
* [Criptografia do lado do cliente e o Cofre da Chave do Azure para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md)

  Este artigo fornece uma explicação de criptografia do lado do cliente e fornece exemplos de uso Olá armazenamento cliente tooencrypt e descriptografar recursos da biblioteca de serviços de armazenamento quatro hello. Ele também fala sobre o Cofre de Chaves do Azure.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Usando a criptografia de disco do Azure tooencrypt discos usados por suas máquinas virtuais
O Azure Disk Encryption é um novo recurso. Esse recurso permite que você tooencrypt Olá OS discos e dados usados por uma máquina Virtual IaaS. Para Windows, Olá unidades são criptografadas usando a tecnologia de criptografia do BitLocker padrão da indústria. Para o Linux, discos de saudação são criptografados usando a tecnologia de saudação DM Crypt. Isso é integrado com o Azure Key Vault tooallow você toocontrol e gerenciar chaves de criptografia de disco hello.

solução de saudação dá suporte à saudação os seguintes cenários para VMs de IaaS quando eles estão habilitados no Microsoft Azure:

* Integração com o Cofre da Chave do Azure
* VMs da camada Standard: [VMs IaaS das séries A, D, DS, G, GS e assim por diante](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Como habilitar a criptografia em VMs IaaS Windows e Linux
* Como desabilitar a criptografia em unidades do sistema operacional e de dados para VMs IaaS do Windows
* Como desabilitar a criptografia em unidades de dados para VMs IaaS do Linux
* Ativando a criptografia em VMs IaaS que estão executando o sistema operacional cliente Windows
* Como habilitar a criptografia em volumes com caminhos de montagem
* Habilitação da criptografia em VMs do Linux que estão configuradas com distribuição de discos (RAID) usando o mdadm
* Como habilitar a criptografia em VMs do Linux usando LVM para discos de dados
* Ativando a criptografia em VMs do Windows que são configurados usando espaços de armazenamento
* Há suporte para todas as regiões públicas do Azure

solução de saudação não oferece suporte a saudação tecnologia versão hello, recursos e cenários a seguir:

* VMs IaaS da camada Básica
* Como desabilitar a criptografia em unidades do sistema operacional para VMs IaaS do Linux
* VMs de IaaS que são criadas usando o método de criação de VM clássico Olá
* Integração com o Serviço de Gerenciamento de Chaves no local
* Armazenamento de Arquivos do Azure (sistema de arquivos compartilhados), NFS (Network File System), volumes dinâmicos e VMs do Windows configuradas com Sistemas RAID baseados em software


> [!NOTE]
> Criptografia de disco do sistema operacional Linux é suportada atualmente no hello seguindo as distribuições do Linux: RHEL 7.2, CentOS 7.2n e 16.04 do Ubuntu.
>
>

Esse recurso garante que todos os dados nos discos da máquina virtual sejam criptografados em repouso no Armazenamento do Azure.

#### <a name="resources"></a>Recursos
* [Azure Disk Encryption para VMs IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Comparação do Azure Disk Encryption, da SSE e da Criptografia do Cliente
#### <a name="iaas-vms-and-their-vhd-files"></a>VMs IaaS e seus arquivos VHD
Para discos usados pelas VMs IaaS, é recomendável usar o Azure Disk Encryption. Você pode ativar SSE tooencrypt Olá arquivos VHD usado tooback desses discos no armazenamento do Azure, mas ele só criptografa dados recém-criados. Isso significa que se você cria uma máquina virtual e, em seguida, habilitar SSE na conta de armazenamento Olá que contém o arquivo VHD hello, somente as alterações de saudação serão criptografadas, Olá não o arquivo VHD original.

Se você criar uma máquina virtual usando uma imagem de saudação do Azure Marketplace, o Azure executa uma [shallow cópia](https://en.wikipedia.org/wiki/Object_copying) de saudação imagem tooyour conta de armazenamento no armazenamento do Azure e ele não é criptografada mesmo se você tiver habilitado o SSE. Depois que ele cria Olá VM e inicia a atualização de imagem Olá, SSE iniciará a criptografia de dados de saudação. Por esse motivo, é melhor toouse que criptografia de disco do Azure em máquinas virtuais criada de imagens em hello Azure Marketplace se você deseja que eles totalmente criptografado.

Se você colocar uma VM criptografada no Azure do local, você será ser capaz de tooupload Olá criptografia chaves tooAzure Cofre de chaves e continuar usando a criptografia de saudação para a VM que você estava usando no local. Criptografia de disco do Azure é toohandle habilitado neste cenário.

Se você tiver não criptografadas VHD do local, você pode carregá-lo na Galeria do hello como uma imagem personalizada e provisionar uma VM dele. Se você fizer isso usando modelos do Gerenciador de recursos de hello, você pode pedir-tooturn na criptografia de disco do Azure quando ele é inicializado Olá VM.

Quando você adiciona um disco de dados e montá-lo em Olá VM, você pode ativar a criptografia de disco do Azure nesse disco de dados. Ela criptografará primeiro esse disco de dados localmente e, em seguida, camada de gerenciamento de serviço Olá fará uma gravação lenta em relação ao armazenamento para que conteúdo de armazenamento de saudação é criptografado.

#### <a name="client-side-encryption"></a>Criptografia do cliente
Criptografia do lado do cliente é o método mais seguro Olá criptografar seus dados, porque ele criptografa-os antes de trânsito e criptografa Olá dados em repouso. No entanto, ele requer que você adicione código tooyour aplicativos usando o armazenamento, que talvez não seja toodo. Nesses casos, você pode usar HTTPs para os dados em trânsito e SSE tooencrypt Olá em repouso.

Com a criptografia do cliente, você pode criptografar entidades de tabela, mensagens da fila e blobs. Com a SSE, você pode criptografar apenas os blobs. Se você precisar de tabela e fila toobe dados criptografado, você deve usar a criptografia do lado do cliente.

Criptografia do lado do cliente é totalmente gerenciada pelo aplicativo hello. Este é o método mais seguro de hello, mas exigir aplicativos de tooyour alterações programático toomake e implementar processos de gerenciamento de chaves. Você usaria isso quando você quiser Olá segurança adicional durante o trânsito e você deseja que seu toobe dados armazenados criptografado.

Criptografia do lado do cliente é mais carga no cliente hello e tiver tooaccount para isso em seus planos de escalabilidade, especialmente se você estiver criptografando e transferindo muitos dados.

#### <a name="storage-service-encryption-sse"></a>SSE (Criptografia do Serviço de Armazenamento)
A SSE é gerenciada pelo Armazenamento do Azure. Usar SSE não oferece segurança Olá dos dados de saudação em trânsito, mas ele criptografa dados saudação conforme eles são gravados tooAzure armazenamento. Não há nenhum impacto no desempenho de saudação ao usar esse recurso.

Você pode criptografar apenas os blobs de blocos, os blobs de acréscimo e os blobs de páginas usando a SSE. Se você precisar de dados de tabela tooencrypt ou fila, você deve considerar usando a criptografia do lado do cliente.

Se você tiver um arquivo ou uma biblioteca de arquivos VHD que você pode usar como base para a criação de novas máquinas virtuais, criar uma nova conta de armazenamento, habilitar SSE e, em seguida, carregar conta de toothat de arquivos VHD hello. Esses arquivos VHD serão criptografados pelo Armazenamento do Azure.

Se você tiver habilitado para discos de saudação em uma máquina virtual e SSE habilitada na conta de armazenamento Olá mantendo Olá arquivos VHD de criptografia de disco do Azure, ele funcionará bem; resultará em quaisquer dados gravados recentemente que estão sendo criptografados duas vezes.

## <a name="storage-analytics"></a>Análise de Armazenamento
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Usando o tipo de análise de armazenamento de autorização toomonitor
Para cada conta de armazenamento, você pode habilitar o log de tooperform de análise de armazenamento do Azure e armazenar dados de métricas. Isso é uma excelente ferramenta toouse quando você deseja métricas de desempenho de saudação toocheck de uma conta de armazenamento, ou precisa tootroubleshoot uma conta de armazenamento porque está com problemas de desempenho.

Outra parte dos dados que você pode ver nos logs de análise de armazenamento Olá é o método de autenticação de saudação usado por alguém ao acessar o armazenamento. Por exemplo, com o armazenamento de Blob, você pode ver se usavam uma assinatura de acesso compartilhado ou chaves de conta de armazenamento hello, ou se o blob Olá acessado foi pública.

Isso pode ser muito útil se você está estreitamente preservando toostorage de acesso. Por exemplo, no armazenamento de Blob, você pode definir todos Olá contêineres tooprivate e implementar o uso de saudação de um serviço SAS ao longo de seus aplicativos. Em seguida, você pode verificar Olá regularmente logs toosee se seus blobs acessados usando chaves de conta de armazenamento hello, que podem indicar uma violação de segurança, ou se blobs Olá são públicos, mas eles não devem ser.

#### <a name="what-do-hello-logs-look-like"></a>O que hello logs aparência?
Depois de habilitar as métricas de conta de armazenamento hello e registro em log por meio de saudação portal do Azure, dados de análise serão iniciado tooaccumulate rapidamente. registro de saudação e métricas para cada serviço é separado; log de saudação só é gravado quando houver atividade na conta de armazenamento, enquanto as métricas de saudação serão registradas a cada minuto, a cada hora ou diariamente, dependendo de como você configura.

Olá logs são armazenados em blobs de blocos em um contêiner chamado $logs na conta de armazenamento hello. Esse contêiner é criado automaticamente quando a Análise de Armazenamento é habilitada. Uma vez criado, esse contêiner não pode ser excluído, embora você possa excluir seu conteúdo.

No contêiner de saudação $logs, há uma pasta para cada serviço e, em seguida, há subpastas para Olá ano/mês/dia/hora. Em hora, Olá logs simplesmente são numeradas. Isso é que hello será semelhante a estrutura de diretórios:

![Exibição dos arquivos de log](./media/storage-security-guide/image1.png)

Cada solicitação tooAzure armazenamento é registrado. Aqui está um instantâneo de um arquivo de log, mostrando Olá primeiro alguns campos.

![Instantâneo de um arquivo de log](./media/storage-security-guide/image2.png)

Você pode ver que você pode usar Olá logs tootrack qualquer tipo de conta de armazenamento tooa de chamadas.

#### <a name="what-are-all-of-those-fields-for"></a>Para que servem todos esses campos?
Há um artigo listado em recursos de saudação abaixo que fornece a lista de saudação de saudação muitos campos na Olá logs e que elas são usadas para. Aqui está a lista de saudação de campos na ordem:

![Instantâneo de campos em um arquivo de log](./media/storage-security-guide/image3.png)

Estamos interessados em entradas de saudação para GetBlob e como eles são autenticados, portanto precisamos toolook para entradas com o tipo de operação "Get-Blob" e verifique o status de solicitação de saudação (4<sup>th</sup> coluna) e o tipo de autorização hello (8<sup>th</sup> coluna).

Por exemplo, em Olá primeiro algumas linhas na listagem de saudação acima, Olá-status da solicitação é "Êxito" e tipo de autorização Olá é "autenticado". Isso significa que a solicitação Olá foi validada usando a chave de conta de armazenamento hello.

#### <a name="how-are-my-blobs-being-authenticated"></a>Como meu blobs estão sendo autenticados?
Temos três casos que nos interessam.

1. Olá blob é público e que são acessadas usando uma URL sem uma assinatura de acesso compartilhado. Nesse caso, status de solicitação de saudação é "AnonymousSuccess" e tipo de autorização Olá é "anônimo".

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. blob de saudação é privado e foi usado com uma assinatura de acesso compartilhado. Nesse caso, status de solicitação de saudação é "SASSuccess" e tipo de autorização de saudação é "sas".

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. blob Olá é particular e chave de armazenamento de saudação foi usado tooaccess-lo. Nesse caso, o status de solicitação de saudação é "**êxito**"e é de tipo de autorização hello"**autenticado**".

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

Você pode usar o hello Microsoft Message Analyzer tooview e analisar esses logs. Ele inclui recursos de pesquisa e filtro. Por exemplo, convém toosearch para instâncias de GetBlob toosee se o uso de saudação é o esperado, toomake ou seja, se alguém não está acessando sua conta de armazenamento inadequadamente.

#### <a name="resources"></a>Recursos
* [Análise de Armazenamento](storage-analytics.md)

  Este artigo é uma visão geral da análise de armazenamento e como tooenable-los.
* [Formato de Log de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Este artigo ilustra Olá formato de Log de análise de armazenamento e detalhes Olá campos disponíveis neste documento, incluindo tipo de autenticação, que indica o tipo de saudação de autenticação usado para a solicitação de saudação.
* [Monitorar uma conta de armazenamento Olá portal do Azure](storage-monitor-storage-account.md)

  Este artigo mostra como tooconfigure de métricas de monitoramento e registro em log para uma conta de armazenamento.
* [Solução de problemas ponta a ponta usando Métricas de Armazenamento do Azure e Registro em Log, AzCopy e Analisador de Mensagem](storage-e2e-troubleshooting.md)

  Este artigo fala sobre como solucionar problemas usando Olá análise de armazenamento e mostra como toouse Olá Microsoft Message Analyzer.
* [Guia Operacional do Analisador de Mensagem da Microsoft](https://technet.microsoft.com/library/jj649776.aspx)

  Este artigo é referência Olá Olá Microsoft Message Analyzer e inclui o tutorial de tooa links, o início rápido e o resumo de recursos.

## <a name="cross-origin-resource-sharing-cors"></a>CORS (Compartilhamento de Recursos entre Origens)
### <a name="cross-domain-access-of-resources"></a>Acesso de recursos entre domínios
Quando um navegador da Web em execução em um domínio faz uma solicitação HTTP a um recurso de outro domínio, isso é chamado de solicitação HTTP entre origens. Por exemplo, uma página HTML no site da contoso.com faz uma solicitação para um jpeg hospedado em fabrikam.blob.core.windows.net. Por motivos de segurança, os navegadores restringem as solicitações HTTP entre origens iniciadas dentro de scripts, como JavaScript. Isso significa que, quando um código JavaScript em uma página da web em contoso.com solicita que jpeg em fabrikam.blob.core.windows.net, navegador Olá não permitirá solicitação hello.

O que faz isso ter toodo com armazenamento do Azure? Bem, se você estiver armazenando ativos estáticos, como arquivos de dados XML ou JSON no armazenamento de Blob usar uma conta de armazenamento chamado Fabrikam, Olá ativos Olá será fabrikam.blob.core.windows.net e aplicativo de web hello contoso.com não será capaz de tooaccess-los usando JavaScript porque Olá domínios são diferentes. Isso também é verdadeiro se você estiver tentando toocall uma saudação serviços de armazenamento do Azure – como o armazenamento de tabela – que retorne JSON dados toobe processada pelo cliente de JavaScript hello.

#### <a name="possible-solutions"></a>Soluções possíveis
Uma maneira tooresolve trata tooassign um domínio personalizado como toofabrikam.blob.core.windows.net "storage.contoso.com". problema de saudação é que você só pode atribuir a conta de armazenamento tooone domínio personalizado. Se os recursos de saudação são armazenados em várias contas de armazenamento?

Outro tooresolve de maneira trata toohave Olá web aplicativo atuar como um proxy para chamadas de armazenamento hello. Isso significa que se você estiver carregando um arquivo tooBlob armazenamento, aplicativo da web hello seria o gravá-la localmente e, em seguida, copie-o tooBlob armazenamento ou ele seria ler tudo na memória e em seguida, escrever tooBlob armazenamento. Como alternativa, você poderia escrever um aplicativo da web dedicado (como uma API da Web) que carrega arquivos Olá localmente e os grava tooBlob armazenamento. De qualquer forma, você tem tooaccount para essa função quando as necessidades de escalabilidade de saudação determinante.

#### <a name="how-can-cors-help"></a>Como o CORS pode ajudar?
Armazenamento do Azure permite que você tooenable CORS – entre o compartilhamento de recursos de origem. Para cada conta de armazenamento, você pode especificar os domínios que podem acessar recursos de saudação na conta de armazenamento. Por exemplo, em nosso caso descrito acima, podemos pode habilitar o CORS na conta de armazenamento fabrikam.blob.core.windows.net Olá e configure-a como tooallow toocontoso.com de acesso. Em seguida, Olá web aplicativo contoso.com pode acessar diretamente os recursos de Olá em fabrikam.blob.core.windows.net.

Um toonote de coisa é que o CORS permite o acesso, mas ele não fornece autenticação, que é necessária para todos os não-acesso público de recursos de armazenamento. Isso significa que você só pode acessar blobs se eles são públicos ou incluir uma assinatura de acesso compartilhado que está fornecendo Olá permissão apropriada. Arquivos, filas e tabelas não têm acesso público e exigem uma SAS.

Por padrão, o CORS está desabilitado em todos os serviços Você pode habilitar o CORS usando Olá API REST ou hello armazenamento cliente biblioteca toocall uma saudação métodos tooset Olá políticas de QoS. Ao fazer isso, você inclui uma regra de CORS, que está em XML. Aqui está um exemplo de uma regra CORS que foi definida usando a operação de definir propriedades de serviço de saudação para Olá serviço Blob para uma conta de armazenamento. Você pode executar essa operação usando a biblioteca de cliente de armazenamento de hello ou Olá APIs REST para armazenamento do Azure.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Veja o que cada linha significa:

* **AllowedOrigins** isso informa quais domínios não correspondentes podem solicitar e receber dados do serviço de armazenamento de saudação. Isso significa que contoso.com e fabrikam.com podem solicitar dados do Armazenamento de Blobs para uma conta de armazenamento específica. Você também pode definir este curinga tooa (\*) tooallow tooaccess de domínios de todas as solicitações.
* **AllowedMethods** esta é a lista Olá dos métodos (verbos de solicitação HTTP) que pode ser usado ao fazer a solicitação de saudação. Neste exemplo, apenas PUT e GET são permitidos. Você pode definir este curinga tooa (\*) tooallow toobe de todos os métodos usados.
* **AllowedHeaders** trata solicitação Olá cabeçalhos que Olá domínio de origem podem especificar ao fazer a solicitação de saudação. No exemplo acima, todos os cabeçalhos de metadados, começando com x-ms-meta-data, x-ms-meta-target e x-ms-meta-abc, são permitidos. Olá caractere curinga (\*) indica que todos os cabeçalhos que começam com hello especificado é permitido um prefixo.
* **ExposedHeaders** isso informa quais cabeçalhos de resposta devem ser expostos por um emissor da solicitação Olá navegador toohello. Neste exemplo, qualquer cabeçalho que começar com "x-ms-meta-" será exposto.
* **MaxAgeInSeconds** este é o período de tempo que um navegador armazenará em cache solicitação OPTIONS da simulação Olá máximo hello. (Para obter mais informações sobre a solicitação de simulação hello, verifique Olá primeiro artigo abaixo).

#### <a name="resources"></a>Recursos
Para obter mais informações sobre CORS e como tooenable-lo, faça check-out desses recursos.

* [Suporte a compartilhamento de recursos entre origens (CORS) Olá serviços de armazenamento do Azure em Azure.com](storage-cors-support.md)

  Este artigo fornece uma visão geral de CORS e como Olá tooset as regras para serviços de armazenamento diferentes de saudação.
* [Suporte a compartilhamento de recursos entre origens (CORS) Olá serviços de armazenamento do Azure no MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Isso é a documentação de referência de saudação para suporte CORS para serviços de armazenamento do Azure hello. Isso traz links tooarticles aplicando tooeach serviço de armazenamento e mostra um exemplo e explica cada elemento no arquivo CORS hello.
* [Microsoft Azure Storage: Introducing CORS (Armazenamento do Microsoft Azure: introdução ao CORS)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Este é um artigo de blog inicial link toohello anunciando CORS e mostrando como toouse-lo.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Perguntas frequentes sobre a segurança do Armazenamento do Azure
1. **Como verificar a integridade de blobs Olá que eu estou transferir para dentro ou fora do armazenamento do Azure se não é possível usar o protocolo HTTPS de saudação Olá?**

   Se por algum motivo, você precisa toouse HTTP em vez de HTTPS e você estiver trabalhando com blobs de bloco, você pode usar a verificação MD5 toohelp verificar a integridade de saudação de blobs Olá que estão sendo transferidos. Isso ajudará na proteção contra erros na camada de rede/transporte, mas não necessariamente contra ataques de intermediários.

   Se você puder usar HTTPS, que fornece segurança em nível de transporte, o uso da verificação MD5 será redundante e desnecessário.

   Para obter mais informações, faça check-out Olá [visão geral do MD5 de Blob do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **E quanto a conformidade com FIPS para os EUA Olá norte-americano?**

   Olá Estados Unidos Federal Information Processing Standard (FIPS) define o algoritmo de criptografia aprovado para uso dos EUA Sistemas de computador do governo federal para proteção de saudação de dados confidenciais. Habilitando FIPS o modo em um servidor do Windows ou a área de trabalho informa Olá SO que algoritmos criptográficos validados de FIPS somente devem ser usados. Se um aplicativo usa algoritmos não compatíveis, aplicativos de saudação serão interrompido. Versões com o.NET Framework 4.5.2 ou superior, aplicativo hello alterna automaticamente algoritmos de toouse compatível com FIPS de algoritmos de criptografia hello quando o computador hello está no modo FIPS.

   Microsoft deixa o tooeach cliente toodecide se tooenable o modo FIPS. Acreditamos que não há nenhum motivo convincente para os clientes que não estão em modo FIPS tooenable do assunto toogovernment regulamentos por padrão.

   **Recursos**

* [Por que não estamos recomendando mais o "Modo FIPS"](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  Esse artigo de blog fornece uma visão geral do FIPS e explica por que o modo FIPS não é habilitado por padrão.
* [FIPS 140 Validation (Validação do FIPS 140)](https://technet.microsoft.com/library/cc750357.aspx)

  Este artigo fornece informações sobre como produtos da Microsoft e módulos de criptografia compatíveis com hello FIPS padrão para os EUA Olá federal dos EUA.
* ["Criptografia de sistema: usar algoritmos em conformidade com o FIPS para criptografia, hash e assinatura", efeitos das configurações de segurança no Windows XP e em versões posteriores do Windows](https://support.microsoft.com/kb/811833)

  Este artigo fala sobre o uso de saudação do modo FIPS computadores Windows mais antigos.
