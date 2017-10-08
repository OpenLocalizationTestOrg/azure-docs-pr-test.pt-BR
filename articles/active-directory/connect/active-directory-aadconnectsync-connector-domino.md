---
title: aaaLotus Domino conector | Microsoft Docs
description: Este artigo descreve como Lotus Domino conector do Microsoft tooconfigure.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Referência técnica do conector Lotus Domino
Este artigo descreve Olá Lotus Domino conector. artigo Olá aplica toohello produtos a seguir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * É necessário usar o hotfix 4.1.3671.0 ou posterior [KB3092178](https://support.microsoft.com/kb/3092178).

Para MIM2016 e FIM2010R2, Olá Connector está disponível como um download do hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Visão geral da saudação conector do Lotus Domino
Olá Lotus Domino conector permite serviço de sincronização de saudação toointegrate com o servidor do IBM Lotus Domino.

De uma perspectiva de alto nível, Olá recursos a seguir é suportado pela versão atual de saudação do conector hello:

| Recurso | Suporte |
| --- | --- |
| Fonte de dados conectada |Servidor:  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Cliente:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Cenários |<li>Gerenciamento de ciclo de vida do objeto</li><li>Gerenciamento de grupos</li><li>Gerenciamento de senha</li> |
| Operações |<li>Importação completa e Delta</li><li>Exportação</li><li>Definir e alterar a senha em senha HTTP</li> |
| Esquema |<li>Pessoa (Roaming do usuário, Contato (pessoas sem certificado))</li><li>Agrupar</li><li>Recurso (Recurso, Reunião online, Sala)</li><li>Banco de dados Entrada de Email</li><li>Descoberta dinâmica de atributos para objetos com suporte</li> |

conector do Lotus Domino Olá usa Olá Lotus Notes cliente toocommunicate com servidor Lotus Domino. Como resultado dessa dependência, um Lotus Notes Client com suporte deve ser instalado no servidor de sincronização de saudação. comunicação de saudação entre cliente hello e servidor de saudação é implementada por meio de interface de interoperabilidade de .NET do Lotus Notes (Interop.domino.dll) hello. Essa interface facilita a comunicação de saudação entre plataformas do Microsoft.NET hello e cliente Lotus Notes e dá suporte a acesso tooLotus Domino documentos e exibições. Para a importação de delta, também é possível que interface Olá C++ nativo é usado (dependendo do método de importação de delta Olá selecionado).

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar o conector de saudação, verifique se que você tem Olá pré-requisitos no servidor de sincronização de saudação a seguir:

* Microsoft .NET 4.5.2 Framework ou posterior
* cliente do Lotus Notes Olá deve ser instalado em seu servidor de sincronização
* Olá Lotus Domino conector requer saudação padrão Lotus Domino LDAP esquema banco de dados (schema.nsf) toobe presente no servidor de diretório Domino hello. Se não estiver presente, você pode instalá-lo executando ou reiniciando o serviço LDAP Olá no servidor do hello Domino.

### <a name="connected-data-source-permissions"></a>Permissões da fonte de dados conectada
tooperform qualquer Olá suporte tarefas no conector Lotus Domino, você deve ser um membro dos seguintes grupos:

* Administradores com acesso completo
* Administradores
* Administradores de banco de dados

Hello tabela a seguir lista as permissões de saudação que são necessárias para cada operação:

| Operação | Direitos de acesso |
| --- | --- |
| Importar |<li>Ler documentos públicos</li><li> Acesso de administrador completo (quando você for membro do grupo de administradores de acesso completo, você automaticamente tem Olá acesso efetivo tooin ACL.)</li> |
| Exportar e definir senha |Acesso efetivo:  <li>Criar documentos</li><li>Excluir documentos</li><li>Ler documentos públicos</li><li>Gravar documentos públicos</li><li>Replicar ou copiar documentos</li>Para operações de exportação, você também precisa Olá funções a seguir: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Operações diretas e AdminP
As operações vá diretamente toohello diretório de Domino ou por meio de saudação AdminP processam. Olá, tabelas a seguir listam todos os objetos com suporte, as operações e, se aplicável, Olá relacionados ao método de implementação:

**Catálogo de endereços principal**

| Objeto | Criação | Atualização | Exclusão |
| --- | --- | --- | --- |
| Pessoa |AdminP |Direta |AdminP |
| Agrupar |AdminP |Direta |AdminP |
| MailInDB |Direta |Direta |Direta |
| Recurso |AdminP |Direta |AdminP |

**Catálogo de endereços secundário**

| Objeto | Criação | Atualização | Exclusão |
| --- | --- | --- | --- |
| Pessoa |N/D |Direta |Direta |
| Agrupar |Direta |Direta |Direta |
| MailInDB |Direta |Direta |Direta |
| Recurso |N/D |N/D |N/D |

Quando um recurso é criado, um documento do Notes é criado. Da mesma forma, quando um recurso for excluído, o documento de notas Olá é excluído.

### <a name="ports-and-protocols"></a>Portas e protocolos
O cliente IBM Lotus Notes e os servidores Domino se comunicam usando a NRPC (Chamada de Procedimento Remoto do Notes), em que NRPC deve usar TCP/IP. número da porta padrão Olá é 1352, mas pode ser alterado pelo administrador do Domino hello.

### <a name="not-supported"></a>Sem suporte
Olá operações a seguir não é suportado pela versão atual de saudação do conector do Lotus Domino hello:

* Mover caixa de correio entre servidores.

## <a name="create-a-new-connector"></a>Criar um novo conector
### <a name="client-software-installation-and-configuration"></a>Instalação e configuração do software cliente
Lotus Notes deve ser instalado no servidor de saudação **antes de** Olá Connector está instalado.

Ao fazer a instalação, tenha a certeza de fazer uma **Instalação de usuário único**. Olá padrão **multiusuário instalar** não funciona.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Na página de recursos do hello, instalar somente Olá necessária recursos do Lotus Notes e **de Logon único do cliente**. Logon único é necessário para Olá conector toobe capaz de toolog no toohello Domino server.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Observação:** início Lotus Notes depois que um usuário que está localizado em Olá mesmo servidor Olá conta que você usar como conta de serviço do conector de hello. Também verifique se cliente do tooclose Olá Lotus Notes no servidor de saudação. Ele não pode ser executado em Olá Olá de tempo mesmo conector tenta tooconnect toohello Domino server.

### <a name="create-connector"></a>Criar o conector
tooCreate um conector Lotus Domino, na **serviço de sincronização** selecione **Management Agent** e **criar**. Selecione Olá **Lotus Domino (Microsoft)** conector.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Se sua versão do serviço de sincronização oferece Olá capacidade tooconfigure **arquitetura**, certifique-se de conector Olá é definido tooits padrão valor toorun na **processo**.

### <a name="connectivity"></a>Conectividade
Na página de conectividade hello, você deve especificar o nome do servidor Lotus Domino Olá e insira as credenciais de logon de saudação.  
![Conectividade](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Olá propriedade servidor Domino dá suporte a dois formatos de nome do servidor de saudação:

* ServerName
* ServerName/DirectoryName

Olá **ServerName/DirectoryName** é formato preferencial de saudação para este atributo porque ele fornece uma resposta mais rápida quando contatos de conector Olá Olá servidor Domino.

Olá fornecido UserID arquivo é armazenado no banco de dados de configuração de saudação do serviço de sincronização de saudação.

Na **Importação Delta** , você tem estas opções:

* **Nenhum**. Olá conector não importações delta.
* **Adicionar/Atualizar**. importação de delta Olá conector faz adicionar e operações de atualização. Para excluir, é necessária uma operação **Importação Completa** . Esta operação está usando interoperabilidade de .net hello.
* **Adicionar/Atualizar/Excluir**. importação de delta Olá conector faz adicionar, atualizar e excluir operações. Esta operação está usando interfaces de C++ nativo hello.

Em **opções de esquema** ter Olá as opções a seguir:

* **Esquema Padrão**. Olá conector detecta o esquema de saudação do servidor do hello Domino. Essa seleção é a opção padrão de saudação.
* **Esquema DSML**. Usado somente se o servidor de Domino Olá não expõe esquema hello. Você pode criar um arquivo DSML com esquema hello e importá-lo em vez disso. Para obter mais informações sobre o DSML, confira [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Quando você clicar em Avançar, Olá UserID e parâmetros de configuração de senha são verificados.

### <a name="global-parameters"></a>Parâmetros Globais
Na página de parâmetros globais hello, configure Olá fuso horário e importar hello e opção de operação de exportação.  
![Parâmetros Globais](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Olá **fuso horário servidor Domino** parâmetro define o local de saudação do servidor Domino.

Essa opção de configuração é necessária toosupport **importação delta** operações porque ela permite que o serviço de sincronização de saudação determinar alterações entre duas últimas importações hello.

>[!Note]
Iniciando na tela de parâmetros globais Olá março de 2017 atualização Olá inclui o banco de dados de email do usuário do hello toodelete opção Olá durante a exclusão do usuário Olá.

![Excluir a caixa de correio de um usuário](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Configurações de importação, método
Olá **executar importação completa por** tem as seguintes opções:

* Pesquisar
* Exibição (Recomendado)

**Pesquisa** é usando a indexação no Domino, mas é comum que índices Olá não são atualizados em tempo real e dados Olá retornados do servidor de saudação sempre não estão corretos. Em um sistema com muitas alterações, essa opção geralmente não funciona bem e fornece exclusões falsas em algumas situações. No entanto, a **pesquisa** é mais rápida que a **exibição**.

**Exibição** Olá recomenda opção porque ele fornece o estado correto de saudação de dados. Ela é ligeiramente mais lenta que a pesquisa.

#### <a name="creation-of-virtual-contact-objects"></a>Criação de objetos Contato Virtual
Olá **permitir a criação de \_objeto contato** tem as seguintes opções:

* Nenhum
* Valores de Não Referência
* Valores de Referência e Não Referência

Domino, atributos de referência podem conter tooreference de formatos diferentes de muitos outros objetos. toobe toorepresent capaz de diferentes variações, Olá implementa conector \_entre em contato com objetos, também conhecido como **contatos Virtual** (VC). Esses objetos são criados para que elas possam ingressar tooexisting MV objetos ou projetados como novos objetos. Dessa forma, as referências de atributo podem ser preservadas.

Ao habilitar essa configuração e se o conteúdo de saudação de um atributo de referência não é um formato de DN, um \_objeto de contato é criado. Por exemplo, um atributo de membro de um grupo pode conter endereços SMTP. Também é possível toohave shortName e outros atributos presentes em atributos de referência. Para esse cenário, selecione **Valores de Não Referência**. Essa configuração é a configuração mais comum Olá para implementações Domino.

Quando Lotus Domino é endereços separados toohave configurados com diferentes nomes distintos que representa Olá mesmo objeto, tooalso possível é criar \_objetos de contato para todos os valores de referência que se encontram em um catálogo de endereços. Para este cenário, selecione Olá **referência e os valores de referência não** opção.

Se você tiver vários valores no atributo Olá **FullName** Domino, em seguida, você deseja tooenable criação de saudação de contatos Virtual para referências possam ser resolvidas. Por exemplo, esse atributo pode ter vários valores após um casamento ou divórcio. Selecione a caixa de seleção Olá **habilitar... FullName tem vários valores** para esse cenário.

Unindo-se em atributos corretos hello, Olá \_objetos de contato seria objeto toohello unidas MV.

Esses objetos têm VC =\_contato adicionado tootheir DN.

#### <a name="import-settings-conflict-object"></a>Configurações de importação, objeto de conflito
**Excluir Objeto de Conflito**

Em uma implementação Domino grande, é possível que vários objetos têm Olá mesmo DN devido a problemas de tooreplication. Nesses casos, o conector Olá veria dois objetos com UniversalIDs diferente, mas mesmo DN. Esse conflito faria com que um objeto temporário sendo criado no espaço do conector hello. Olá conector pode ignorar objetos Olá selecionados Domino como vítimas de replicação. recomendação de saudação é tookeep essa caixa de seleção é selecionada.

#### <a name="export-settings"></a>Exportar configurações
Se hello opção **AdminP usar para atualizar referências** estiver desmarcada, a exportação de atributos de referência, como membros, uma chamada direta e não usa o processo de AdminP hello. Só use essa opção quando AdminP não foi configurado toomaintain a integridade referencial.

#### <a name="routing-information"></a>Informações de roteamento
Domino, é possível que um atributo de referência tem informações de roteamento inseridas como um sufixo toohello DN. Por exemplo, o atributo de membro de saudação em um grupo pode conter **CN =example/organization@ABC**. sufixo de saudação @ABC Olá informações de roteamento. informações de roteamento Hello são usadas por Domino toosend emails toohello Domino sistema correto, que pode ser um sistema em uma organização diferente. No campo de informações de roteamento hello, você pode especificar usado dentro da organização Olá no escopo da saudação conector roteamento de sufixos de saudação. Se um desses valores é encontrado como um sufixo em um atributo de referência, as informações de roteamento Olá serão removidas da referência de saudação. Se o sufixo de roteamento de saudação em um valor de referência não pode ser correspondido tooone desses valores especificados, um \_objeto de contato é criado. Essas \_objetos de contato são criados com **RO = @<RoutingSuffix>**  inseridos Olá DN. Essas \_objetos de contato Olá atributos a seguir também é adicionados tooallow unindo o objeto real tooa se necessário: \_routingName, \_contactName, \_displayName e UniversalID.

#### <a name="additional-address-books"></a>Catálogos de endereços adicionais
Se você não tem **auxílio** instalado, que fornece o nome de saudação do endereços secundários, e em seguida, você pode inserir manualmente esses endereços.

#### <a name="multivalued-transformation"></a>Transformação com vários valores
Muitos atributos no Lotus Domino têm vários valores. Olá atributos correspondentes do metaverso são normalmente único valor. Configurando Olá importação e a opção de operação de exportação hello, você habilitar Olá conector toohelp com conversão de Olá necessárias dos atributos de saudação afetado.

**Exportarar**  
opção de operação de exportação Olá dá suporte a dois modos:

* Acrescentar item
* Substituir item

**Substituir Item** – quando você seleciona essa opção, o conector de saudação sempre remover Olá atual valores de atributo Olá Domino e substituí-los com valores hello fornecido. Olá fornecido com valor pode ser um valor único ou múltiplos.

Exemplo: o atributo de Assistente de saudação do objeto de uma pessoa tem Olá valores a seguir:

* CN=Vinicius Monte/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Paulo Araújo/OU=Contoso/O=Americas,NAB=names.nsf

Se um novo assistente denominado **David Alexander** é atribuído o objeto de pessoa toothis, o resultado de saudação é:

* CN=Pedro Gonçalves/OU=Contoso/O=Americas,NAB=names.nsf

**Acrescentar um Item** – quando você seleciona essa opção, conector Olá retém os valores existentes no atributo Olá Domino e inserir novos valores na parte superior de saudação da lista de dados Olá Olá.

Exemplo: o atributo de Assistente de saudação do objeto de uma pessoa tem Olá valores a seguir:

* CN=Vinicius Monte/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Paulo Araújo/OU=Contoso/O=Americas,NAB=names.nsf

Se um novo assistente denominado **David Alexander** é atribuído o objeto de pessoa toothis, o resultado de saudação é:

* CN=Pedro Gonçalves/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Vinicius Monte/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Paulo Araújo/OU=Contoso/O=Americas,NAB=names.nsf

**Importaçãoação**  
opção de operação de importação de saudação suporta dois modos:

* Padrão
* Valor de múltiplos valores tooSingle

**Padrão** – quando você seleciona a opção padrão de saudação, todos os valores da saudação todos os atributos são importados.

**Valor de múltiplos valores tooSingle** – quando você seleciona essa opção, um atributo com valores múltiplos é convertido em um atributo de valor único. Se houver mais de um valor, o valor de saudação na parte superior de saudação (esse valor é normalmente também hello mais recente) é usado.

Exemplo: o atributo de Assistente de saudação do objeto de uma pessoa tem Olá valores a seguir:

* CN=Pedro Gonçalves/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Vinicius Monte/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Paulo Araújo/OU=Contoso/O=Americas,NAB=names.nsf

Hello mais recente atualização toothis atributo é **David Alexander**. Como opção de operação de importação de saudação é definida tooMultivalued tooSingle valor, conector importa somente **David Alexander** no espaço do conector de saudação.

tooconvert de lógica de saudação múltiplos atributos em atributos de valor único não se aplicam toohello grupo membro e toohello pessoa fullname atributo.

Ele também tooconfigure possível importar e exportar regras de transformação de atributos multivalorados por atributo, como uma regra de exceção global de toohello. tooconfigure essa opção, digite [objecttype]. [attributename] no hello **importar a lista de atributos de exclusão** e **exportar a lista de atributos de exclusão** caixas de texto. Por exemplo, se você digitar Person.Assistant e sinalizador global Olá for definido tooimport todos os valores, o único valor de primeira Olá é importado para o Assistente de saudação.

#### <a name="certifiers"></a>Certificadores
Todas as unidades organizacionais/organização são listadas pelo conector hello. catálogo toobe tooexport capaz de pessoa objetos toohello endereço primário, um certifier com sua senha é necessária.

Se tem todos os certifiers Olá mesma senha, hello **senha para todos os Certifers** pode ser usado. Você pode inserir Olá senha aqui e especificar apenas o arquivo de certifier hello.

Se você importar somente, em seguida, você não tem toospecify qualquer certifiers.

### <a name="configure-provisioning-hierarchy"></a>Configurar a hierarquia de provisionamento
Quando você configura o conector do Lotus Domino hello, ignore essa página da caixa de diálogo. conector do Lotus Domino Olá não dá suporte a hierarquia de provisionamento.  
![Hierarquia de provisionamento](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurar partições e hierarquias
Quando você configura partições e hierarquias, você deve selecionar o catálogo de endereço primário Olá chamado NAB=names.nsf. Além disso toohello catálogo de endereço primário, você pode selecionar endereços secundários se existirem.  
![Partições](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Selecionar atributos
Ao configurar atributos, você deve selecionar todos os atributos que tenham o prefixo **\_MMS\_**. Esses atributos são necessários quando você provisionar novos objetos tooLotus Domino

![Atributos](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Gerenciamento de ciclo de vida do objeto
Esta seção fornece uma visão geral de objetos diferentes de saudação Domino.

### <a name="person-objects"></a>Objetos de pessoa
objeto de pessoa Olá representa usuários na organização e unidades organizacionais. Além disso, atributos de padrão de toohello, administrador do Domino Olá podem adicionar objeto de pessoa tooa atributos personalizados. No mínimo, um objeto Person deve incluir todos os atributos obrigatórios. Para obter uma lista completa de atributos obrigatórios, confira [Propriedades do Lotus Notes](#lotus-notes-properties). tooregister objeto de uma pessoa, Olá pré-requisitos a seguir deve ser atendido:

* Catálogo de endereços da saudação (names.nsf) deve ter definido e deve ser Olá principal de endereços.
* Você deve ter um usuário específico de Olá O/UO certifier Id e hello senha tooregister em Olá organização / unidade organizacional.
* É preciso definir um conjunto específico de propriedades do Lotus Notes para um objeto de pessoa. Essas propriedades são usadas para o provisionamento de objeto de pessoa hello. Para obter mais informações, consulte a seção Olá chamada [propriedades do Lotus Notes](#lotus-notes-properties) mais adiante neste documento.
* senha de uma pessoa do saudação inicial HTTP é um atributo e um conjunto durante o provisionamento.
* objeto de pessoa Olá deve ser um dos seguintes três tipos com suporte de saudação:
  1. Usuário Normal que tenha um arquivo de email e um arquivo de id de usuário
  2. Usuário móvel (um Usuário Normal que inclua todos os arquivos de banco de dados móvel)
  3. Contatos (usuário sem arquivo de id)

Pessoas (exceto contatos) adicionais podem ser agrupadas nos usuários e internacionais conforme definido pelo valor Olá Olá \_MMS\_IDRegType propriedade. Essas pessoas usam Olá cliente Notes tooaccess servidores Lotus Domino, ter uma Id de notas e um documento de pessoa. Se estiverem usando o email do Notes, eles também terão um arquivo de email. usuário Olá deve ser registrado toobecome ativo. Para obter mais informações, consulte:

* [Setting up Notes users](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [User Registration](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Managing users](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Renaming users](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Todas essas operações são executadas no Lotus Domino e, em seguida, importadas para o serviço de sincronização de saudação.

### <a name="resources-and-rooms"></a>Recursos e salas
Um Recurso é outro tipo de banco de dados do Lotus Domino. Os Recursos podem ser salas de conferência com vários tipos de equipamento, como projetores. Há subtipos de recursos com suporte pelo conector Lotus Domino que são definidos pelo atributo de tipo de recurso de saudação:

| Tipo de recurso | Atributo Tipo de Recurso |
| --- | --- |
| Sala |1 |
| Recurso (Outros) |2 |
| Reunião Online |3 |

Para toowork de tipo de objeto de recurso hello, Olá é necessário:

* Banco de dados de reserva de recursos já deve existir no servidor de Domino Olá conectado
* site de saudação já está definida para Olá recursos

banco de dados de reserva de recurso Olá contém três tipos de documentos:

* Perfil do Site
* Recurso
* Reserva

Para obter mais informações sobre a configuração de banco de dados de reserva de recursos, consulte [configurar banco de dados de recurso reservas Olá](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Criar, atualizar e excluir recursos**  
Olá operações Create, Update e Delete são executadas pelo conector do Lotus Domino Olá no banco de dados de reserva de recurso hello. Recursos são criados como documentos em Names.nsf (ou seja, catálogo de endereço primário Olá). Para obter mais informações sobre como editar e excluir Recursos, confira [Editando e excluindo documentos do Recurso](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html).

**Operação Importar e Exportar para Recursos**  
Olá recursos pode ser importado tooand exportado do serviço de sincronização de saudação, como qualquer outro tipo de objeto. Tipo de objeto Olá selecione como recursos durante a configuração. Para que a operação de exportação seja bem-sucedida, você deve ter detalhes do tipo Recurso, Banco de Dados de Conferência e Nome do site.

### <a name="mail-in-databases"></a>Bancos de dados de Entrada de Email
Um email no banco de dados é um banco de dados é projetado tooreceive emails. Trata-se de uma caixa de correio do Lotus Domino que não está associada a qualquer conta de usuário específica do Lotus Domino (isto é, não tem seu próprio arquivo de ID e senha). Um banco de dados de Entrada de Email tem um UserID exclusivo (“nome curto”) associado a ele e seu próprio endereço de email.

Se houver a necessidade de uma caixa de correio separada com seu próprio endereço de email que possa ser compartilhada entre usuários diferentes (por exemplo: group@contoso.com), um banco de dados de entrada de email será criado. caixa de correio do Hello acesso toothis é controlada por meio de seu controle de acesso lista (ACL), que contém os nomes de saudação de usuários de anotações Olá que têm permissão de caixa de correio tooopen Olá.

Para obter uma lista de atributos de saudação necessários, consulte seção Olá chamada [atributos obrigatórios](#mandatory-attributes) posteriormente neste artigo.

Quando um banco de dados é projetado tooreceive um email, um documento de email no banco de dados é criado no Lotus Domino. Este documento deve existir no diretório de Domino de cada servidor que armazena uma cópia do banco de dados de saudação. Para obter uma descrição detalhada sobre como criar um documento de banco de dados de entrada de email, confira [Creating a Mail-In Database document](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)(Criando um documento de banco de dados de entrada de email).

Antes de criar um banco de dados de correio, o banco de dados de saudação já deve existir (deve ter sido criado pelo administrador do Lotus) no servidor do hello Domino.

### <a name="group-management"></a>Gerenciamento de grupos
Você pode obter uma visão geral do gerenciamento de grupo do Lotus Domino saudação do hello recursos a seguir:

* [Using groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Creating a group](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Creating and modifying groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Managing groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Renaming a group](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Gerenciamento de senha
Para um usuário registrado do Lotus Domino, existem dois tipos de senha:

1. Senha do usuário (armazenada no arquivo User.id)
2. Senha Internet/HTTP

conector do Lotus Domino Olá suporta somente operações com senha HTTP.

gerenciamento de senha tooperform, você deve habilitar o gerenciamento de senha para o conector de saudação em hello Designer do agente de gerenciamento. gerenciamento de senha tooenable, selecione **habilitar o gerenciamento de senha** em Olá **configurar extensões** página da caixa de diálogo.  
![Configurar Extensões](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Olá Lotus Domino conector suporte operações de senha da Internet a seguir:

* Definir senha: Definir senha define uma nova senha HTTP/Internet no usuário Olá Domino. Por padrão a conta Olá também está desbloqueada. Olá desbloquear sinalizador é exposto na interface de WMI Olá Olá mecanismo de sincronização.
* Alterar senha: Nesse cenário, um usuário poderá toochange senha de saudação ou é solicitada toochange senha após um tempo especificado. Para este local de tootake de operação, tanto (Olá antiga e nova senha de saudação) são obrigatórios. Depois de alterado, a nova senha de saudação será atualizada no Lotus Domino.

Para obter mais informações, consulte:

* [Usando o recurso de bloqueio de Internet Olá](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Managing Internet passwords](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Informações de referência
Esta seção lista como requisitos de atributo para o conector do Lotus Domino hello e descrições de atributo.

### <a name="lotus-notes-properties"></a>Propriedades do Lotus Notes
Ao configurar o diretório de Lotus Domino pessoa objetos tooyour, os objetos devem ter um conjunto específico de propriedades com valores específicos preenchidos. Esses valores só serão necessários para as operações Create.

Olá tabela a seguir lista essas propriedades e fornece uma descrição deles.

| Propriedade | Descrição |
| --- | --- |
| \_MMS_AltFullName |Olá alternativo nome completo do usuário. |
| \_MMS_AltFullNameLanguage |Olá toobe de idioma usado para especificar o nome completo alternativo de saudação do usuário. |
| \_MMS_CertDaysToExpire |número de saudação de dias da saudação data atual antes do certificado de saudação expira. Se não for especificado, data de padrão de saudação é de dois anos de saudação data atual. |
| \_MMS_Certifier |Propriedade que contém o nome de hierarquia organizacional de saudação do certifier hello. Por exemplo: OU=OrganizationUnit,O=Org,C=Country. |
| \_MMS_IDPath |Se a propriedade Olá estiver vazia, nenhum arquivo de identificação do usuário é criado localmente no servidor de sincronização de saudação. Se a propriedade Olá contém um nome de arquivo, um arquivo de ID de usuário é criado na pasta de madata de saudação. propriedade Olá também pode conter um caminho completo. |
| \__MMS_IDRegType |As pessoas podem ser classificadas como contatos, Usuários dos EUA e Usuários internacionais. Olá tabela a seguir lista os valores possíveis hello: <li>0 - Contato</li><li>1 - Usuário dos EUA</li><li>2 - Usuário internacional</li> |
| \_MMS_IDStoreType |Propriedade necessária para os usuários dos EUA e internacionais. propriedade Olá contém um valor inteiro que especifica se a identificação de saudação do usuário é armazenada como um anexo no catálogo de endereços do hello notas ou no arquivo de email da pessoa hello. Se o arquivo de ID de usuário de saudação um anexo no catálogo de endereços do hello, pode opcionalmente ser criado como um arquivo com \_MMS_IDPath. <li>Vazio — arquivo de ID do repositório no Cofre de ID, nenhum arquivo de identificação (usado para Contatos).</li><li> 1 - anexo no catálogo de endereços do hello anotações. Olá \_MMS_Password propriedade deve ser definida para arquivos de identificação de usuário que são anexos</li><li>2 - ID do repositório no arquivo de email da pessoa. Olá \_MMS_UseAdminP deve ser definido como mensagens de saudação do toofalse toolet arquivo ser criado durante a saudação registro pessoa. Olá \_MMS_Password propriedade deve ser definida para arquivos de identificação de usuário.</li> |
| \_MMS_MailQuotaSizeLimit |número de saudação de megabytes que são permitidos para o banco de dados do arquivo hello email. |
| \_MMS_MailQuotaWarningThreshold |número de saudação de megabytes permitido para o banco de dados do arquivo hello email antes que um aviso será emitido. |
| \_MMS_MailTemplateName |Olá email arquivo de modelo que é o arquivo de email do usuário de saudação toocreate usado. Se um modelo for especificado, o arquivo de email Olá é criado usando o modelo especificado hello. Se nenhum modelo for especificado, Olá padrão modelo é usado toocreate Olá arquivo. |
| \_MMS_OU |Propriedade opcional que é nome da UO Olá em certifier hello. Essa propriedade deve estar vazia para os contatos. |
| \_MMS_Password |A propriedade necessária para os usuários. propriedade Olá contém senha Olá para o arquivo de identificação de saudação do objeto hello. |
| \_MMS_UseAdminP |Propriedade deve ser o conjunto tootrue se o arquivo de email Olá deve ser criado pelo processo de AdminP Olá no servidor Domino de saudação (processo de exportação toohello assíncrona). Se a propriedade for definida toofalse, Olá mail arquivo é criado com hello usuário Domino (síncrona no processo de exportação de saudação). |

Para um usuário com um arquivo de identificação associado, Olá \_propriedade MMS_Password deve conter um valor. Para acesso de email por meio do cliente Lotus Notes hello, hello MailServer e MailFile propriedades de um usuário devem conter um valor.

tooaccess de email por meio de um navegador da Web, Olá propriedades a seguir deve conter valores:

* MailFile - propriedade necessária que contém Olá caminho no servidor do Lotus Domino Olá onde Olá mail arquivo está armazenado.
* Servidor de email - propriedade necessária que contém o nome de saudação do servidor do Lotus Domino hello. Esse valor é Olá nome toouse ao criar arquivo de email Olá Lotus no servidor do hello Domino.
* HTTPPassword - propriedade opcional que contém a senha de acesso Web Olá para objeto hello.

tooaccess Olá servidor Domino sem recurso de email, Olá propriedade HTTPPassword deve conter um valor. Olá propriedade MailFile e Olá propriedade MailServer pode ficar vazio.

Com \_MMS_ IDStoreType = 2 (id do repositório no arquivo de email), Olá propriedade MailSystem NotesRegistrationclass está definida tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Atributos obrigatórios
conector do Lotus Domino Olá principalmente dá suporte a esses tipos de objetos (tipos de documento):

* Agrupar
* Banco de dados Entrada de Email
* Pessoa
* Contato (Indivíduo sem certificador)
* Recurso

Esta seção lista os atributos de saudação são obrigatórios para cada servidor do objeto com suporte tooexport tooa Domino.

| Tipo de objeto | Atributos obrigatórios |
| --- | --- |
| Agrupar |<li>ListName</li> |
| Banco de dados de Entrada de Email |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Pessoa |<li>Sobrenome</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\__MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Contato (Indivíduo sem certificador) |<li>\__MMS_IDRegType</li> |
| Recurso |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Site</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Problemas e perguntas comuns
### <a name="schema-detection-does-not-work"></a>Detecção de esquema não funciona
esquema de saudação do toobe toodetect capaz, é necessário que arquivo hello schema.nsf está presente no servidor de Domino de saudação. Esse arquivo só aparecerá se LDAP está instalado no servidor de saudação. Se Olá esquema não é detectável, verifique se a seguir hello:

* Olá arquivo schema.nsf está presente na pasta raiz de saudação do hello servidor Domino
* usuário Olá tem arquivo de schema.nsf permissões toosee hello.
* Força a reinicialização do servidor de saudação do LDAP. Abra **Lotus Domino Console** e usar **dizer LDAP ReloadSchema** esquema de saudação do comando tooreload.

### <a name="not-all-secondary-address-books-are-visible"></a>Nem todos os catálogos de endereços secundários estão visíveis
Olá Domino conector depende do recurso de saudação **auxílio** toobe toofind capaz de saudação secundário endereços. Se os endereços secundários Olá estiverem ausentes, verifique se [auxílio](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) foi habilitado e configurado no servidor Domino de saudação.

### <a name="custom-attributes-in-domino"></a>Atributos personalizados no Domino
Há várias maneiras no esquema de saudação do Domino tooextend, então ele aparece como um atributo personalizado pode ser consumido por Olá conector.

**Abordagem 1: Estender o esquema do Lotus Domino**

1. Criar uma cópia do modelo do diretório Domino {PUBNAMES. NTF} seguindo [essas etapas](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (você não deve personalizar diretório IBM Lotus Domino de padrão Olá modelo):
2. Modelo de diretório de cópia de Domino abrir Olá {CONTOSO. Modelo NTF} que foi criado no Designer de Domino e siga estas etapas:
   * Clique em Elementos Compartilhados e expanda os Subformulários
   * Clique duas vezes em subformulário de InheritableSchema ${ObjectName} (onde {ObjectName} é nome Olá Olá padrão estrutural da classe de objeto, por exemplo: pessoa).
   * Nomear atributo Olá deseja tooadd em esquema {MyPersonAtrribute} e o atributo toothat correspondente. Criar um campo, selecione Olá **criar** Menu e selecione **campo** no menu.
   * No campo adicionado do hello, defina suas propriedades selecionando seu tipo, estilo, tamanho, fonte e outros parâmetros relacionados na janela de propriedades de campo.
   * Manter atributo de saudação padrão mesmo valor fornecido para o atributo de nome de saudação (por exemplo, se o nome do atributo é MyPersonAttribute, manter valor padrão de saudação com hello mesmo nome).
   * Salve subformulário do hello ${ObjectName} InheritableSchema com valores atualizados.
3. Substituir saudação Domino Directory modelo {PUBNAMES. NTF} com o modelo personalizado novo Olá {CONTOSO. NTF} seguindo [essas etapas](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Fechar Domino administrador e abra saudação do Console Domino toorestart serviço LDAP e Olá tooReload esquema LDAP:
   * No Console do Domino, inserir o comando de saudação em **comando Domino** texto arquivado, o serviço do protocolo LDAP Olá toorestart - [reiniciar tarefa LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * esquema LDAP tooreload usar o comando de informar LDAP - informar ReloadSchema de LDAP
5. Abra Domino Admin e selecione toosee de guia de pessoas e grupos adicionados atributo é refletido no domino adicionar pessoa.
6. Abra Schema.nsf na guia **Arquivos** e veja se o atributo adicionado é refletido na classe do objeto LDAP dominoPerson.

**Método 2: Criar um auxClass com atributo personalizado e associar com a classe de objeto Olá**

1. Criar uma cópia do modelo do diretório Domino {PUBNAMES. NTF} seguindo [essas etapas](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (nunca personalize o diretório de IBM Lotus Domino saudação padrão modelo):
2. Modelo de diretório de cópia de Domino abrir Olá {CONTOSO. Modelo NTF} foi criado, no Designer de Domino.
3. No painel esquerdo do hello, selecione o código compartilhado e, em seguida, subformulários.
4. Clique em Novo Subformulário
5. Olá toospecify Olá propriedades subformulário novo Olá a seguir:
   * Com subformulário novo Olá aberto, escolha Design - propriedades de subformulário
   * Toohello próxima propriedade Name, insira um nome para a classe de objeto auxiliar hello – por exemplo, TestSubform.
   * Manter a propriedade de opções de hello "Incluir no subformulário Insert... caixa de diálogo" selecionada
   * Desmarque a propriedade Options de hello "Renderização passar HTML em anotações."
   * Deixe Olá outras propriedades Olá mesmo e feche a caixa de propriedades de subformulário Olá.
   * Salve e feche o subformulário novo hello.
6. Olá tooadd uma classe de objeto auxiliar do campo toodefine Olá a seguir:
   * Abra o subformulário Olá criado por você.
   * Escolha Criar - Campo.
   * Próxima tooName na guia de Noções básicas de Olá Olá campo da caixa de diálogo, especifique qualquer nome, por exemplo: {MyPersonTestAttribute}.
   * No campo adicionado do hello, defina suas propriedades, selecionando o tipo, estilo, tamanho, fonte e suas propriedades relacionadas.
   * Manter atributo de saudação padrão mesmo valor fornecido para o atributo de nome de saudação (por exemplo, se o nome do atributo é MyPersonTestAttribute, manter valor padrão de saudação com hello mesmo nome).
   * Salvar subformulário Olá com valores atualizados e Olá a seguir:
     * No painel esquerdo do hello, selecione o código compartilhado e, em seguida, subformulários
     * Selecione subformulário novo hello e escolha Design - propriedades de Design.
     * Clique a terceira guia Olá da saudação esquerda e selecione **propagar essa proibição de alteração de design**.
7. Abra o subformulário de ExtensibleSchema ${ObjectName}, (onde {ObjectName} é o nome Olá Olá padrão estrutural da classe de objeto, por exemplo – pessoa).
8. Inserir recurso Olá subformulário (que você criou, por exemplo – TestSubform) e selecione Salvar subformulário de ExtensibleSchema ${ObjectName} hello.
9. Substituir saudação Domino Directory modelo {PUBNAMES. NTF} com o modelo personalizado novo Olá {CONTOSO. NTF} seguindo [essas etapas](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Fechar Domino administrador e abra saudação do Console Domino toorestart serviço LDAP e Olá tooReload esquema LDAP:
    * No Console do Domino, inserir o comando de saudação em **comando Domino** texto arquivado, o serviço do protocolo LDAP Olá toorestart - [reiniciar tarefa LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * esquema LDAP tooreload usar o comando LDAP informar **dizer LDAP ReloadSchema**.
11. Abra Domino Admin e selecione toosee de guia de pessoas e grupos adicionados atributo é refletido no domino adicionar pessoa (em outras guia).
12. Abra Schema.nsf na guia **Arquivos** e veja se o atributo adicionado é refletido sob a classe de objeto auxiliar TestSubform LDAP.

**Abordagem 3: Adicionar classe de ExtensibleObject de toohello Olá atributo personalizado**

1. Abrir arquivo {Schema.nsf} colocado no diretório raiz de saudação
2. Selecione as Classes de objeto LDAP no menu esquerdo de saudação em **todos os documentos de esquema** e clique em **classe adicionar objeto** botão:
3. Forneça o nome de LDAP no formulário de saudação do {zzzExtensibleSchema} (em que zzz é nome Olá Olá padrão estrutural da classe de objeto, por exemplo pessoa). Por exemplo, o esquema de saudação tooextend para a classe de objeto de pessoa, forneça o nome LDAP {PersonExtensibleSchema}.
4. Forneça o nome de classe do objeto Superior, para o qual você deseja que o esquema de saudação tooextend. Por exemplo, o esquema de saudação tooextend para a classe de objeto de pessoa, fornecer nome de classe do objeto Superior {dominoPerson}:
5. Fornece uma classe de objeto de toohello válida correspondente OID.
6. Selecione os atributos estendidos/personalizados em campos obrigatório ou opcional tipos de atributo de acordo com o requisito de saudação:
7. Depois de adicionar necessário atributos toohello ExtensibleObjectClass, clique em **Salvar & Fechar**.
8. Uma ExtensibleObjectClass é criada para a classe de objeto padrão respectiva com atributos estendidos.

## <a name="troubleshooting"></a>Solucionar problemas
* Para obter informações sobre como o log tooenable tootroubleshoot Olá conector, consulte Olá [como tooEnable o rastreamento ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
