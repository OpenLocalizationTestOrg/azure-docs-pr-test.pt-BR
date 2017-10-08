---
title: aaaGeneric conector LDAP | Microsoft Docs
description: "Este artigo descreve como conector LDAP genérico de tooconfigure da Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Referência técnica do Conector LDAP genérico
Este artigo descreve Olá genérico conector de LDAP. artigo Olá aplica toohello produtos a seguir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * É necessário usar o hotfix 4.1.3671.0 ou posterior [KB3092178](https://support.microsoft.com/kb/3092178).

Para MIM2016 e FIM2010R2, Olá Connector está disponível como um download do hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Ao fazer referência tooIETF RFCs, este documento está usando o formato de saudação (RFC [número RFC] / [seção no documento RFC]), por exemplo (RFC 4512/4.3).
Você pode encontrar mais informações em http://tools.ietf.org/html/rfc4500 (é necessário tooreplace 4500 com o número correto de RFC Olá).

## <a name="overview-of-hello-generic-ldap-connector"></a>Visão geral da saudação conector de LDAP genérico
Olá conector de LDAP genérico permite que você toointegrate Olá serviço de sincronização com um servidor do LDAP v3.

Determinadas operações e os elementos do esquema, como aqueles necessários tooperform importação de delta, não são especificados na Olá IETF RFCs. Para essas operações, apenas os diretórios LDAP especificados explicitamente recebem suporte.

De uma perspectiva de alto nível, Olá recursos a seguir é suportado pela versão atual de saudação do conector hello:

| Recurso | Suporte |
| --- | --- |
| Fonte de dados conectada |Olá conector é compatível com todos os servidores do LDAP v3 (compatível com RFC 4510). Ela foi testada com a seguinte hello: <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Catálogo Global do Microsoft Active Directory (AD GC)</li><li>Directory Server 389</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (antiga Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**Não há suporte para diretórios notáveis:** <li>Microsoft Active Directory Domain Services (AD DS) [Use Olá conector interno do Active Directory em vez disso]</li><li>Oracle Internet Directory (OID)</li> |
| Cenários |<li>Gerenciamento de ciclo de vida do objeto</li><li>Gerenciamento de grupos</li><li>Gerenciamento de senha</li> |
| Operações |Olá seguintes operações têm suporte em todos os diretórios LDAP: <li>Importação completa</li><li>Exportação</li>Olá seguintes operações têm suporte somente nos diretórios especificados:<li>Importação delta</li><li>Definir senha, alterar senha</li> |
| Esquema |<li>Esquema for detectado do esquema LDAP hello (RFC3673 e RFC4512/4.2)</li><li>Oferece suporte a classes estruturais, classes auxiliares e à classe de objeto extensibleObject (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Suporte de gerenciamento de importação delta e de senha
Diretórios com suporte para gerenciamento de importação delta e de senha:

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição de senha
* Catálogo Global do Microsoft Active Directory (AD GC)
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição de senha
* Directory Server 389
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Apache Directory Server
  * Não oferece suporte para importação delta, pois esse diretório não tem um log de alteração persistente
  * Oferece suporte para definição de senha
* IBM Tivoli DS
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Isode Directory
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Novell eDirectory e NetIQ eDirectory
  * Oferece suporte para operações de adição, atualização e renomeação para importação delta
  * Não oferece suporte para operações de exclusão para importação delta
  * Oferece suporte para definição e alteração de senha
* Open DJ
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Open DS
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Open LDAP (openldap.org)
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição de senha
  * Não oferece suporte para alteração de senha
* Oracle (antiga Sun) Directory Server Enterprise Edition
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* RadiantOne Virtual Directory Server (VDS)
  * Deve usar a versão 7.1.1 ou superior
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha
* Sun One Directory Server
  * Oferece suporte para todas as operações de importação delta
  * Oferece suporte para definição e alteração de senha

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar o conector de saudação, verifique se que você tem o seguinte Olá no servidor de sincronização de saudação:

* Microsoft .NET 4.5.2 Framework ou posterior

### <a name="detecting-hello-ldap-server"></a>Detecção de servidor do LDAP Olá
depende de vários toodetect de técnicas de saudação conector e identificar o servidor LDAP de saudação. Olá conector usa Olá DSE de raiz, versão/nome do fornecedor, e ele inspeciona objetos exclusivos da saudação esquema toofind e atributos conhecidos tooexist em determinados servidores LDAP. Esses dados, se encontrado, é usado toopre-preencher as opções de configuração de saudação do hello conector.

### <a name="connected-data-source-permissions"></a>Permissões da fonte de dados conectada
tooperform importar e exportar operações em objetos de saudação no diretório conectado hello, conta de saudação do conector deve ter permissões suficientes. conector Olá precisa gravar permissões toobe capaz de tooexport e tooimport capaz de toobe permissões de leitura. Configuração de permissão é executada em experiências de gerenciamento de saudação do diretório de destino de saudação em si.

### <a name="ports-and-protocols"></a>Portas e protocolos
conector de Olá usa o número da porta Olá especificado na configuração de saudação, que por padrão é 389 para LDAP e 636 para LDAP.

Para LDAPS, você deve usar SSL 3.0 ou TLS. Não há suporte para SSL 2.0 e não é possível ativá-lo.

### <a name="required-controls-and-features"></a>Recursos e controles necessários
Olá LDAP seguintes controles/recursos devem estar disponíveis no servidor do LDAP Olá para Olá conector toowork corretamente:  
`1.3.6.1.4.1.4203.1.5.3` Verdadeiro/Falso

filtro de verdadeiro/falso Olá frequentemente não é relatado como diretórios LDAP com suporte e pode aparecer em Olá **página Global** em **obrigatório recursos não encontrado**. Ele é usado toocreate **ou** filtros em consultas LDAP, por exemplo, durante a importação de vários tipos de objeto. Se você puder importar mais de um tipo de objeto, seu servidor LDAP dará suporte a esse recurso.

Se você usar um diretório em que é um identificador exclusivo a seguir Olá âncora Olá também deve estar disponível (para obter mais informações, consulte Olá [configurar âncoras](#configure-anchors) seção):  
`1.3.6.1.4.1.4203.1.5.1` todos os atributos operacionais

Se o diretório de saudação mais objetos que o que pode caber em um diretório de toohello de chamada, em seguida, é recomendável toouse paginação. Toowork de paginação, é necessário um Olá as opções a seguir:

**Opção 1:**  
`1.2.840.113556.1.4.319` pagedResultsControl

**Opção 2:**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

Se as duas opções são habilitadas na configuração de conector hello, pagedResultsControl será usado.

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl é usado somente com hello USNChanged delta importar método toobe toosee capaz de excluir objetos.

conector de saudação tenta toodetect de opções de saudação presente no servidor de saudação. Se as opções de saudação não podem ser detectadas, um aviso está presente no página Global Olá nas propriedades do conector hello. Nem todos os servidores LDAP todos os controles de recursos/eles dão suporte e mesmo se esse aviso estiver presente, Olá conector pode funcionar sem problemas.

### <a name="delta-import"></a>Importação delta
A importação delta só estará disponível quando um diretório de suporte tiver sido detectado. Olá métodos a seguir está sendo usada:

* LDAP Accesslog. Confira [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP Changelog. Confira [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* TimeStamp. Para NetIQ/Novell eDirectory, Olá conector usa última data/hora tooget criado e atualizado objetos. NetIQ/Novell eDirectory não fornece que um equivalente significa tooretrieve excluída objetos. Essa opção também pode ser usada se nenhum outro método de importação de delta estiver ativo no servidor do LDAP hello. Essa opção não é capaz de tooimport excluída objetos.
* USNChanged. Confira: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Sem suporte
Olá recursos LDAP a seguir não têm suporte:

* Referências de LDAP entre servidores (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Criar um novo conector
tooCreate um conector LDAP genérico, na **serviço de sincronização** selecione **Management Agent** e **criar**. Selecione Olá **LDAP genérico (Microsoft)** conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Conectividade
Na página de conectividade hello, você deve especificar informações de Host, porta e associação de saudação. Dependendo de qual associação está selecionado, mais informações podem ser fornecidas na Olá seções a seguir.

![Conectividade](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* configuração de tempo limite de Conexão de saudação somente é usada para o primeiro servidor de toohello conexão Olá ao detectar o esquema de saudação.
* Se a Associação for Anônima, nenhum nome de usuário/senha ou certificado será usado.
* Para outras associações, insira informações em nome de usuário/senha ou escolha um certificado.
* Se você estiver usando o Kerberos tooauthenticate, também fornecem Olá Realm/domínio do usuário de saudação.

Olá **aliases de atributo** caixa de texto é usada para atributos definidos no esquema de saudação com sintaxe RFC4522. Esses atributos não podem ser detectados durante a detecção do esquema e Olá conector precisa de ajuda tooidentify esses atributos. Por exemplo hello seguinte deve ser inserido no hello atributo aliases caixa toocorrectly identificar atributo de userCertificate hello como um atributo binário:

`userCertificate;binary`

a seguir Olá é um exemplo de como essa configuração seria semelhante ao seguinte:

![Conectividade](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Selecione Olá **incluem atributos operacionais no esquema** tooalso da caixa de seleção incluir atributos criados pelo servidor de saudação. Isso inclui atributos, como quando o objeto de saudação foi criado e hora da última atualização.

Selecione **incluem extensíveis atributos no esquema** se objetos extensíveis (RFC4512/4.3) são usados e a habilitação dessa opção permite que cada toobe atributo usado em todos os objetos. Selecionar essa opção torna esquema Olá muito grande, a menos que o diretório conectado hello está usando esta recomendação de saudação do recurso é tookeep Olá opção.

### <a name="global-parameters"></a>Parâmetros Globais
Na página de parâmetros globais hello, configure log de alterações do hello DN toohello delta e os recursos adicionais do LDAP. página de saudação é preenchida previamente com informações de Olá fornecidas pelo servidor do LDAP hello.

![Conectividade](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

seção superior Olá mostra informações fornecidas pelo servidor de saudação em si, como nome de saudação do servidor de saudação. Olá conector também verifica se controles obrigatórios Olá estão presentes no hello DSE de raiz. Se esses controles não estiverem listados, será apresentado um aviso. Alguns diretórios LDAP não listar todos os recursos no hello DSE de raiz e é possível que o hello funciona conector sem problemas, mesmo que haja um aviso.

Olá **suporte para controles** caixas de seleção controlam o comportamento de saudação para determinadas operações:

* Com a opção de exclusão de árvore marcada, uma hierarquia é excluída com uma chamada LDAP. Com a exclusão de árvore desmarcado, conector Olá faz uma exclusão recursiva, se necessário.
* Com resultados paginados selecionados, Olá conector faz uma importação paginada com tamanho de saudação especificado nas etapas Olá executar.
* Olá VLVControl e SortControl é um dado de tooread pagedResultsControl toohello alternativo do diretório LDAP de saudação.
* Se todas as três opções (pagedResultsControl, VLVControl e SortControl) estão desmarcadas hello conector importa todos os objetos em uma única operação, o que poderá falhar se um diretório grande.
* ShowDeletedControl é usado somente quando o método de importação de Delta hello é USNChanged.

o log de alterações de saudação DN é o contexto de nomenclatura Olá usado pelo log de alterações delta hello, por exemplo **cn = log de alterações**. Esse valor deve ser especificado a importação de delta capaz de toodo toobe.

a seguir Olá é uma lista de log de alteração padrão DNs:

| Diretório | Log de alterações delta |
| --- | --- |
| Microsoft AD LDS e AD GC |Detectado automaticamente. USNChanged. |
| Apache Directory Server |Não disponível. |
| Directory 389 |Log de alterações. Padrão de valor toouse: **cn = log de alterações** |
| IBM Tivoli DS |Log de alterações. Padrão de valor toouse: **cn = log de alterações** |
| Isode Directory |Log de alterações. Padrão de valor toouse: **cn = log de alterações** |
| Novell/NetIQ eDirectory |Não disponível. TimeStamp. Olá conector usa última data/hora atualizado tooget adicionado e registros atualizados. |
| Open DJ/DS |Log de alterações.  Padrão de valor toouse: **cn = log de alterações** |
| Open LDAP |Log de acesso. Padrão de valor toouse: **cn = accesslog** |
| Oracle DSEE |Log de alterações. Padrão de valor toouse: **cn = log de alterações** |
| RadiantOne VDS |Diretório virtual. Depende de saudação tooVDS de diretório conectado. |
| Sun One Directory Server |Log de alterações. Padrão de valor toouse: **cn = log de alterações** |

o atributo de senha Olá é nome hello de saudação do atributo de saudação conector deve usar a senha de saudação do tooset em operações de conjunto de senha e alteração de senha.
Esse valor é definido muito por padrão**userPassword** , mas pode ser alterado quando necessário para um determinado sistema LDAP.

Na lista de partições adicionais Olá, é possível tooadd namespaces adicionais detectados automaticamente. Por exemplo, essa configuração pode ser usada se vários servidores compõem um grupo lógico, deve ser importado no hello simultaneamente. Assim como o Active Directory pode ter vários domínios em uma floresta, mas todos os domínios compartilham um esquema, Olá mesmo podem ser simulado inserindo namespaces adicionais Olá nesta caixa. Cada namespace pode importar de diferentes servidores e adicional é configurado na página Configurar partições e hierarquias de saudação. Use Ctrl + Enter tooget uma nova linha.

### <a name="configure-provisioning-hierarchy"></a>Configurar a hierarquia de provisionamento
Essa página está toomap usado Olá DN componente, por exemplo, UO, toohello tipo de objeto que deve ser provisionado, por exemplo, organizationalUnit.

![Hierarquia de Provisionamento](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Ao configurar a hierarquia de provisionamento, você pode configurar Olá conector tooautomatically criar uma estrutura quando necessário. Por exemplo, se houver um controlador de domínio do namespace = contoso, dc = com e um novo cn de objeto = Joe, ou = Seattle, c = US, dc = contoso, dc = com é provisionada e Olá conector pode criar um objeto do país de tipo para os EUA e um organizationalUnit para Seattle se eles não estiverem já no diretório de saudação.

### <a name="configure-partitions-and-hierarchies"></a>Configurar partições e hierarquias
Na página partições e hierarquias hello, selecione todos os namespaces com objetos planejar tooimport e exportação.

![Partições](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Para cada namespace, também é possível tooconfigure configurações de conectividade que poderia substituir valores hello especificados na tela de conectividade de saudação. Se esses valores forem deixados valor em branco do tootheir padrão, informações de saudação da tela de conectividade hello são usadas.

Também é possível tooselect quais contêineres e UOs Olá conector deve importar e exportar para.

Ao realizar uma pesquisa, isso é feito em todos os contêineres na partição de saudação. Em casos onde há grandes números de contêineres esse comportamento leva tooperformance degradação.

>[!NOTE]
A partir do toohello de atualização de março de 2017 Olá LDAP genérico pesquisas de conector podem ser limitadas em contêineres do escopo tooonly Olá selecionado. Isso pode ser feito selecionando a caixa de seleção de saudação 'Pesquisa apenas nos contêineres selecionados' conforme mostrado na imagem de saudação abaixo.

![Pesquisar apenas os contêineres selecionados](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Configurar Âncoras
Essa página sempre têm um valor pré-configurado e não pode ser alterada. Se o fornecedor do servidor de saudação foi identificado, âncora Olá pode estar populada com um atributo imutável, Olá exemplo GUID de um objeto. Se ele não foi detectado ou conhecido toonot ter um atributo imutável, em seguida, conector Olá usa dn (nome distinto) como âncora de saudação.

![âncoras](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


a seguir Olá é uma lista de servidores LDAP e âncora hello está sendo usada:

| Diretório | Atributo de âncora |
| --- | --- |
| Microsoft AD LDS e AD GC |objectGUID |
| Directory Server 389 |dn |
| Apache Directory |dn |
| IBM Tivoli DS |dn |
| Isode Directory |dn |
| Novell/NetIQ eDirectory |GUID |
| Open DJ/DS |dn |
| Open LDAP |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One Directory Server |dn |

## <a name="other-notes"></a>Outras observações
Esta seção fornece informações sobre aspectos específicos toothis conector ou por outros motivos tooknow importante.

### <a name="delta-import"></a>Importação delta
marca d'água delta de saudação em Open LDAP é data/hora UTC. Por esse motivo, relógios Olá entre o serviço de sincronização do FIM e hello Open LDAP devem ser sincronizados. Caso contrário, algumas entradas no log de alterações delta Olá podem ser omitidas.

Para Novell eDirectory, importação de delta hello está detectando não exclui qualquer objeto. Por esse motivo, é necessário toorun completo periodicamente importar excluído toofind todos os objetos.

Para diretórios com um delta alteração do log com base em data/hora, é altamente recomendável toorun uma importação completa em momentos periódicas. Esse processo permite Olá toofind de mecanismo de sincronização e dissimilarities entre o servidor do LDAP hello e que estão atualmente no espaço do conector de saudação.

## <a name="troubleshooting"></a>Solucionar problemas
* Para obter informações sobre como o log tooenable tootroubleshoot Olá conector, consulte Olá [como tooEnable o rastreamento ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
