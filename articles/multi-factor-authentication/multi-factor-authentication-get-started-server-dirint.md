---
title: "aaaDirectory integração entre o Azure multi-Factor Authentication e o Active Directory"
description: "Esta é hello Azure multi-factor authentication página que descreve como toointegrate Olá servidor Azure multi-Factor Authentication com o Active Directory para sincronizar os diretórios de saudação."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Integração de diretórios entre o Azure MFA Server e o Active Directory
Use seção Integração de diretórios Olá Olá servidor Azure MFA toointegrate com o Active Directory ou outro diretório LDAP. Você pode configurar o esquema de diretório atributos toomatch hello e configurar a sincronização automática de usuários.

## <a name="settings"></a>Configurações
Por padrão, Olá servidor Azure multi-Factor Authentication (MFA) é configurado tooimport ou sincronizar usuários do Active Directory.  Guia de integração de diretórios do Hello permite que você toooverride Olá comportamento padrão e diretório LDAP diferente de tooa toobind, um diretório ADAM ou controlador de domínio do Active Directory específico.  Ele também fornece para o uso de saudação de autenticação LDAP tooproxy LDAP ou LDAP Bind como um destino RADIUS, pré-autenticação para autenticação IIS ou autenticação principal para Portal do usuário.  Olá a tabela a seguir descreve as configurações individuais de saudação.

![Configurações](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Recurso | Descrição |
| --- | --- |
| Usar o Active Directory |Selecione toouse de opção de usar o Active Directory de saudação do Active Directory para importação e sincronização.  Essa é a configuração de padrão de saudação. <br>Observação: Para o Active Directory integration toowork corretamente, ingressar Olá computador tooa domínio e entrar usando uma conta de domínio. |
| Incluir domínios confiáveis |Verificar **incluir domínios confiáveis** toohave Olá Agente tentativa tooconnect toodomains confiável Olá domínio atual, outro domínio na floresta de saudação ou domínios envolvidos em uma relação de confiança de floresta.  Quando não importando ou sincronizando usuários de qualquer Olá os domínios confiáveis, desmarque a opção de desempenho de tooimprove de caixa de seleção de saudação.  padrão de saudação é verificada. |
| Usar configuração LDAP específica |Selecione Olá usar LDAP opção toouse Olá configurações LDAP especificadas para importação e sincronização. Observação: Quando usar LDAP estiver selecionada, interface do usuário Olá altera as referências de tooLDAP do Active Directory. |
| Botão Editar |botão de edição Olá permite Olá atual toomodified das configurações da configuração de LDAP. |
| Usar consultas de escopo de atributo |Indica se as consultas de escopo de atributo devem ser usadas.  Permitem consultas de escopo de atributo para pesquisas eficientes de diretórios com base nas entradas de saudação em outro atributo do registro de registros de qualificação.  Olá servidor Azure multi-Factor Authentication usa o atributo escopo consultas tooefficiently consulta Olá usuários que são membros de um grupo de segurança.   <br>Observação: há alguns casos em que há suporte para consultas de escopo de atributo, mas elas não devem ser usadas.  Por exemplo, o Active Directory pode ter problemas com consultas de escopo de atributo quando um grupo de segurança contiver membros de mais de um domínio. Nesse caso, desmarque o caixa de seleção de saudação. |

Olá a tabela a seguir descreve as definições de configuração de LDAP hello.

| Recurso | Descrição |
| --- | --- |
| Servidor |Insira a saudação de nome de host ou endereço IP do servidor de saudação executando o diretório LDAP de saudação.  Um servidor de backup também pode ser especificado separado por ponto-e-vírgula. <br>Observação: quando o Tipo de Associação for SSL, é necessário um nome de host totalmente qualificado. |
| DN base |Digite o nome distinto de Olá Olá base do objeto de diretório do qual iniciam todas as consultas de diretório.  Por exemplo, d=abc,dc=com. |
| Tipo de associação – Consultas |Selecione o tipo de ligação apropriado de Olá para usar ao ligar o diretório LDAP toosearch hello.  Isso é usado para importações, sincronização e resolução de nome de usuário. <br><br>  Anônimo: uma associação anônima será executada.  O DN e associar senha não são usados.  Isso só funcionará se o diretório LDAP de saudação permite associação anônima e permissões permitirem a consulta de saudação de atributos e registros adequados hello.  <br><br> Simples - DN e senha de ligação são passados como o diretório LDAP do texto sem formatação toobind toohello.  Isso é para fins de teste, tooverify que Olá servidor pode ser alcançado e Olá ligação conta tem acesso apropriado do hello. Depois que o certificado apropriado Olá tiver sido instalado, use o SSL.  <br><br> SSL - DN de ligação e a senha de ligação serão criptografados usando SSL toobind toohello LDAP directory.  Instale um certificado localmente que Olá relações de confiança de diretório LDAP.  <br><br> Windows - nome de usuário de ligação e a senha de associação são usada toosecurely conectar controlador de domínio do Active Directory tooan ou diretório ADAM.  Se o nome de usuário de ligação for deixado em branco, a conta de saudação logon do usuário é toobind usado. |
| Tipo de associação – Autenticações |Selecione o tipo de ligação apropriado de saudação para usar ao executar a autenticação de ligação LDAP.  Consulte as descrições de tipo de ligação Olá em tipo de associação - consultas.  Por exemplo, isso permite que toobe ligação anônima usada para consultas enquanto a ligação SSL é usado toosecure as autenticações de ligação LDAP. |
| Associar DN de ligação ou nome de usuário |Digite o nome distinto de saudação de registro de usuário de saudação para Olá conta toouse ao associar um diretório LDAP de toohello.<br><br>nome distinto de ligação Olá só é usado quando o tipo de ligação é simples ou SSL.  <br><br>Insira o nome de usuário de saudação do toouse de conta do Windows hello ao associar o diretório LDAP de toohello quando o tipo de ligação é Windows.  Se deixado em branco, a conta de saudação logon do usuário é toobind usado. |
| Senha de associação |Insira a senha de associação Olá para Olá DN de ligação ou nome de usuário que está sendo o diretório LDAP toohello toobind usado.  senha tooconfigure Olá Olá serviço AdSync do multi-Factor Authentication Server, habilitar a sincronização e certifique-se de que o serviço de saudação está em execução na máquina local hello.  senha de saudação será salva no hello Windows armazenados nomes de usuário e senhas em Olá Olá de conta que serviço AdSync do multi-Factor Auth Server está em execução.  senha Olá também serão salvos em Olá Olá de conta multi-Factor Authentication Server interface do usuário está em execução como e, em Olá Olá de conta serviço servidor multi-Factor Authentication é executado como.  <br><br>Desde que a senha de saudação somente é armazenada no servidor de local Olá nomes de usuário do Windows armazenados e senhas, repita essa etapa em cada servidor de autenticação multifator que precisa de acesso toohello senha. |
| Limite de tamanho de consulta |Especifique o limite de tamanho de saudação para o número máximo de saudação de usuários que retorna uma pesquisa de diretório.  Esse limite deve coincidir com a configuração de Olá no diretório LDAP de saudação.  Para pesquisas maiores onde a paginação não tem suporte, a importação e sincronização tentativas tooretrieve usuários em lotes.  Se o limite de tamanho de saudação especificado aqui for maior que o limite de saudação configurado no diretório LDAP de hello, alguns usuários poderão ser perdidos. |
| Botão de teste |Clique em **teste** servidor LDAP do tootest associação toohello.  <br><br>Não é necessário Olá tooselect **usar LDAP** opção tootest associação. Isso permite Olá associação toobe testada antes de você usa a configuração de LDAP de saudação. |

## <a name="filters"></a>Filtros
Filtros permitem registros de tooqualify tooset critérios ao realizar uma pesquisa de diretório.  Definir filtro hello, você pode definir o escopo Olá objetos que você deseja toosynchronize.  

![Filtros](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Autenticação multifator do Azure tem Olá três opções de filtro a seguir:

* **Filtro de contêiner** -especificar critérios de filtro de saudação usados tooqualify registros de recipientes ao realizar uma pesquisa de diretório.  Para o Active Directory e o ADAM, (| ( objectClass=organizationalUnit)(objectClass=container)) normalmente é usado.  Para outros diretórios LDAP, use os critérios de filtro que qualificam cada tipo de objeto de contêiner, dependendo do esquema de diretório hello.  <br>Observação: se for deixado em branco, ((objectClass=organizationalUnit)(objectClass=container)) será usado por padrão.
* **Filtro de grupo de segurança** -especificar critérios de filtro de saudação usados tooqualify registros de grupo de segurança ao realizar uma pesquisa de diretório.  Para o Active Directory e o ADAM, (&(objectCategory=group) (groupType:1.2.840.113556.1.4.804:=-2147483648)) normalmente é usado.  Para outros diretórios LDAP, use os critérios de filtro que qualificam cada tipo de objeto de grupo de segurança, dependendo do esquema de diretório hello.  <br>Observação: se for deixado em branco, (&(objectCategory=group) (groupType:1.2.840.113556.1.4.804:=-2147483648)) será usado por padrão.
* **Filtro de usuário** -especificar critérios de filtro de saudação usados tooqualify registros de usuário ao realizar uma pesquisa de diretório.  Para o Active Directory e o ADAM, (& (objectClass=user)(objectCategory=person)) normalmente é usado.  Para outros diretórios LDAP, use (objectClass = inetOrgPerson) ou algo semelhante, dependendo do esquema de diretório hello. <br>Observação: se for deixado em branco, (&(objectCategory=person)(objectClass=user)) será usado por padrão.

## <a name="attributes"></a>Atributos
Você pode personalizar atributos como necessário para um diretório específico.  Isso permite que você tooadd os atributos personalizados e ajustar Olá sincronização tooonly Olá atributos necessários. Use o nome de saudação do hello attricute conforme definido no esquema de diretório Olá para o valor de saudação de cada campo de atributo. Olá tabela a seguir fornece informações adicionais sobre cada recurso.

Atributos podem ser inseridos manualmente e não são necessário toomatch um atributo na lista de atributos de saudação.

![Atributos](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Recurso | Descrição |
| --- | --- |
| Identificador exclusivo |Digite o nome do atributo de saudação do atributo Olá que serve como identificador exclusivo de saudação do recipiente, grupo de segurança e registros de usuário.  No Active Directory, isso geralmente é objectGUID. Outras implementações LDAP podem usar entryUUID ou algo semelhante.  saudação padrão é objectGUID. |
| Tipo de identificador exclusivo |Selecione o tipo de saudação do atributo de identificador exclusivo de saudação.  No Active Directory, o atributo do hello objectGUID é do tipo GUID. Outras implementações LDAP podem usar o tipo Cadeia de Caracteres ou Matriz de Bytes ASCII.  saudação padrão é GUID. <br><br>É importante tooset esse tipo corretamente porque os itens de sincronização são referenciados por seu identificador exclusivo. Olá tipo de identificador exclusivo é usado toodirectly localizar Olá directory hello.  TooString esse tipo de configuração ao diretório Olá realmente armazena o valor de saudação como uma matriz de bytes de caracteres ASCII impede que a sincronização funcione corretamente. |
| Nome distinto |Digite o nome do atributo de saudação do atributo Olá que contém o nome distinto de saudação para cada registro.  No Active Directory, isso geralmente é distinguishedName. Outras implementações LDAP podem usar entryDN ou algo semelhante.  saudação padrão é distinguishedName. <br><br>Se um atributo contendo apenas Olá nome diferenciado não existir, atributo adspath de saudação pode ser usado.  Olá "LDAP: / /\<server\>/" parte do caminho de saudação é retirado automaticamente, deixando apenas Olá nome diferenciado do objeto de saudação. |
| Nome do contêiner |Digite o nome do atributo de saudação do atributo Olá que contém o nome da saudação em um registro de contêiner.  valor de saudação desse atributo é exibido na hierarquia de contêiner de saudação durante a importação do Active Directory ou a adição de itens de sincronização.  saudação padrão é nome. <br><br>Se recipientes diferentes usam atributos diferentes para seus nomes, use ponto e vírgula tooseparate vários atributos de nome de contêiner.  primeiro atributo de nome de contêiner Olá localizado em um objeto de contêiner é usado toodisplay seu nome. |
| Nome do grupo de segurança |Digite o nome do atributo de saudação do atributo Olá que contém o nome da saudação em um registro de grupo de segurança.  valor de saudação desse atributo é exibido na lista de grupos de segurança de saudação durante a importação do Active Directory ou a adição de itens de sincronização.  saudação padrão é nome. |
| Nome de Usuário |Digite o nome do atributo de saudação do atributo Olá que contém o nome de usuário de saudação em um registro de usuário.  valor de saudação desse atributo é usado como nome de usuário do servidor multi-Factor Auth hello.  Um segundo atributo pode ser especificado como um backup toohello primeiro.  Olá segundo atributo só é usado se Olá primeiro atributo não contiver um valor para o usuário hello.  Olá padrões são userPrincipalName e sAMAccountName. |
| Nome |Digite o nome do atributo de saudação do atributo Olá que contém nome hello em um registro de usuário.  saudação padrão é givenName. |
| Sobrenome |Digite o nome do atributo de saudação do atributo Olá que contém o sobrenome Olá em um registro de usuário.  saudação padrão é sn. |
| Endereço de email |Digite o nome do atributo de saudação do atributo Olá que contém o endereço de email de saudação em um registro de usuário.  Endereço de email é usado toosend boas-vindas e atualização de usuário de toohello de emails.  saudação padrão é mail. |
| Grupo de usuários |Digite o nome do atributo de saudação do atributo Olá que contém o grupo de usuários de saudação em um registro de usuário.  Grupo de usuários pode ser usado toofilter usuários no agente hello e em relatórios no hello Portal de gerenciamento de servidor de autenticação multifator. |
| Descrição |Digite o nome do atributo de saudação do atributo Olá que contém a descrição de saudação em um registro de usuário.  A descrição é usada somente para pesquisa.  saudação padrão é descrição. |
| Idioma to telefonema |Insira o nome do atributo de saudação do atributo de saudação que contém o nome curto saudação do hello idioma toouse para chamadas de voz do usuário de saudação. |
| Idioma da mensagem de texto |Digite o nome do atributo de saudação do atributo Olá que contém nome curto de saudação do hello idioma toouse para mensagens de texto SMS para o usuário de saudação. |
| Idioma do aplicativo móvel |Digite o nome do atributo de saudação do atributo Olá que contém nome curto de saudação do Olá idioma toouse para mensagens de texto de aplicativo de telefone para usuário hello. |
| Idioma do token OATH |Insira o nome do atributo de saudação do atributo de saudação que contém o nome curto Olá de saudação idioma toouse para mensagens de texto de token OATH do usuário de saudação. |
| Telefone comercial |Digite o nome do atributo de saudação do atributo Olá que contém o número de telefone comercial Olá em um registro de usuário.  saudação padrão é telephoneNumber. |
| Telefone residencial |Digite o nome do atributo de saudação do atributo Olá que contém o número de telefone residencial Olá em um registro de usuário.  saudação padrão é homePhone. |
| Pager |Digite o nome do atributo de saudação do atributo Olá que contém o número do pager Olá em um registro de usuário.  saudação padrão é pager. |
| Telefone celular |Digite o nome do atributo de saudação do atributo Olá que contém o número de telefone celular Olá em um registro de usuário.  saudação padrão é celular. |
| Fax |Digite o nome do atributo de saudação do atributo Olá que contém o número de fax Olá em um registro de usuário.  saudação padrão é facsimileTelephoneNumber. |
| Telefone IP |Digite o nome do atributo de saudação do atributo Olá que contém o número de telefone IP hello em um registro de usuário.  saudação padrão é ipPhone. |
| Personalizado |Digite o nome do atributo de saudação do atributo Olá que contém um número de telefone personalizado em um registro de usuário.  padrão de saudação é em branco. |
| Extensão |Digite o nome do atributo de saudação do atributo Olá que contém a extensão de número de telefone Olá em um registro de usuário.  valor de saudação do campo de extensão de saudação é usado como o número de telefone principal do hello extensão toohello somente.  padrão de saudação é em branco. <br><br>Se o atributo de extensão de saudação não for especificado, as extensões podem ser incluídas como parte do atributo de telefone hello. Nesse caso, preceda extensão Olá com um 'x' para que ele obtém analisado corretamente.  Por exemplo, 555-123-4567 x890 resultaria em 555-123-4567 como número de telefone hello e 890 como extensão de saudação. |
| Botão Restaurar Padrões |Clique em **restaurar padrões** tooreturn tootheir valor de padrão de volta todos os atributos.  Olá padrões devem funcionar corretamente com o esquema do Active Directory ou ADAM normal hello. |

atributos de tooedit, clique em **editar** no guia de atributos de saudação.  Isso abre uma janela onde você pode editar os atributos de saudação. Selecione Olá **...**  tooopen de atributo tooany Avançar uma janela onde você pode escolher quais atributos toodisplay.

![Editar Atributos](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Sincronização
A sincronização mantém os dados de usuário do Azure MFA Olá sincronizado com hello usuários no Active Directory ou outro diretório Lightweight Directory Access Protocol (LDAP). processo de saudação é semelhante usuários tooimporting manualmente a partir do Active Directory, mas periodicamente sonda do usuário do Active Directory e tooprocess as alterações no grupo de segurança.  Ela também desativa ou remove usuários que foram removidos de um contêiner, o grupo de segurança ou o Active Directory.

Olá o serviço ADSync do multi-Factor Auth é um serviço do Windows que executa Olá periódica de sondagem do Active Directory.  Isso não é toobe confundido com a sincronização do AD do Azure ou Azure AD Connect.  Olá ADSync do multi-Factor Auth, embora criado em uma base de código semelhante, é específico toohello servidor Azure multi-Factor Authentication.  Ele é instalado em um estado parado e é iniciado pelo Olá serviço do servidor multi-Factor Auth quando configurado toorun.  Se você tiver uma configuração de servidor multi-Factor Auth multisservidor, Olá ADSync do multi-Factor Auth só pode ser executado em um único servidor.

Olá o serviço ADSync do multi-Factor Auth usa Olá extensão do servidor DirSync LDAP fornecida por sondagem de tooefficiently da Microsoft para que as alterações.  O chamador de controle DirSync deve ter hello "diretório obter alterações" à direita e DS-Replication-Get-Changes controle estendido direito de acesso.  Por padrão, esses direitos são atribuídos toohello contas de administrador e LocalSystem nos controladores de domínio.  Olá o serviço AdSync do multi-Factor Auth é toorun configurado como sistema local por padrão.  Portanto, é mais simples serviço de saudação toorun em um controlador de domínio.  Se você configurar Olá serviço tooalways executar uma sincronização completa, ele pode ser executado como uma conta com menos permissões.  Isso é menos eficiente, mas requer menos privilégios de conta.

Se o diretório LDAP de saudação oferece suporte e está configurado para o DirSync, em seguida, sondagem para alterações do grupo de segurança de usuário e funcionará Olá mesmo como ocorre com o Active Directory.  Se o diretório LDAP de saudação não oferece suporte a saudação controle DirSync, uma sincronização completa é executada durante cada ciclo.

![Sincronização](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Olá tabela a seguir contém informações adicionais sobre cada uma das configurações da guia sincronização hello.

| Recurso | Descrição |
| --- | --- |
| Habilitar a sincronização com o Active Directory |Quando marcada, Olá serviço do servidor multi-Factor Auth periodicamente pesquisa do Active Directory para que as alterações. <br><br>Observação: deve ser adicionado a pelo menos um Item de sincronização e sincronizar agora deve ser executado antes de saudação multi-Factor Authentication Server serviço será iniciado o processamento de alterações. |
| Sincronizar cada |Especifique a saudação de intervalo de tempo Olá multi-Factor Authentication Server serviço aguardará entre a sondagem e processamento de alterações. <br><br> Observação: o intervalo de saudação especificado é tempo de saudação entre o início de saudação de cada ciclo.  Se o processamento de tempo de saudação alterações excederem o intervalo de saudação, serviço Olá pesquisará novamente imediatamente. |
| Remover os usuários não está mais no Active Directory |Quando marcada, Olá serviço do servidor multi-Factor Auth processará marcas de exclusão de usuário excluído do Active Directory e remover Olá relacionados ao servidor multi-Factor Authentication usuário. |
| Sempre executar uma sincronização completa |Quando marcada, Olá serviço do servidor multi-Factor Auth sempre executará uma sincronização completa.  Quando desmarcada, Olá serviço do servidor multi-Factor Auth executará uma sincronização incremental consultando apenas os usuários que foram alterados.  saudação padrão estar desmarcada. <br><br>Quando desmarcada, o servidor Azure MFA executa sincronização incremental somente quando o diretório Olá dá suporte a controle de DirSync hello e o diretório de toohello de associação de conta Olá tem consultas incrementais do DirSync permissões tooperform.  Se Olá conta não tem as permissões apropriadas hello ou diversos domínios estiverem envolvidos na sincronização hello, o servidor Azure MFA executa uma sincronização completa. |
| Exigir a aprovação do administrador quando mais de X usuários forem desabilitados ou removidos |Itens de sincronização podem ser configurado toodisable ou remover usuários que não são mais um membro do grupo de segurança ou o contêiner do item de saudação.  Como proteção, aprovação do administrador pode ser exigida quando o número de saudação de usuários toodisable ou remover excede um limite.  Quando marcada, a opção de aprovação é exigida para o limite especificado.  saudação padrão é 5 e o intervalo de saudação é 1 too999. <br><br> A aprovação é facilitada por enviar primeiro uma tooadministrators de notificação de email. notificação por email Olá fornece instruções para revisar e aprovar a desabilitação de saudação e a remoção de usuários.  Quando a interface de usuário do servidor multi-Factor Auth Olá é iniciado, ele solicitará para aprovação. |

Olá **sincronizar agora** botão permite que você toorun uma sincronização completa para sincronização Olá itens especificados.  Uma sincronização completa é necessária sempre que itens de sincronização são adicionados, modificados, removidos ou reordenados.  Também é Olá necessária antes do serviço AdSync do multi-Factor Auth está operacional, já que ele define saudação do qual Olá serviço votará alterações incrementais de ponto de partida.  Se foram feitas alterações toosynchronization itens, mas ainda não foi executada uma sincronização completa, será solicitado tooSynchronize agora.

Olá **remover** botão permite Olá administrador toodelete um ou mais itens de sincronização da lista de itens de sincronização de servidor multi-Factor Auth hello.

> [!WARNING]
> Depois que um registro de item de sincronização tiver sido removido, ele não pode ser recuperado. Você precisará sincronização de saudação tooadd registro de item novamente se tiver sido excluído por engano.

item de sincronização de saudação ou itens de sincronização foram removidos do servidor multi-Factor Authentication.  saudação de serviço do servidor multi-Factor Auth não processará mais os itens de sincronização de saudação.

botões Mover para cima e mover para baixo de saudação permitem administrador Olá toochange ordem de saudação dos itens de sincronização de saudação.  Olá ordem é importante pois hello mesmo usuário pode ser um membro de mais de um item de sincronização (por exemplo, um contêiner e um grupo de segurança).  configurações de saudação usuário toohello aplicada durante a sincronização virão do primeiro item de sincronização Olá no usuário de Olá Olá lista toowhich está associado.  Portanto, os itens de sincronização Olá devem ser colocados em ordem de prioridade.

> [!TIP]
> Uma sincronização completa deve ser executada após a remoção de itens de sincronização.  Uma sincronização completa deve ser executada após a ordenação dos itens de sincronização.  Clique em **sincronizar agora** tooperform uma sincronização completa.

## <a name="multi-factor-auth-servers"></a>Servidores de autenticação multifator
Servidores adicionais de autenticação multifator pode ser definidos se tooserve como um backup proxy RADIUS, proxy LDAP, ou para a autenticação do IIS. configuração da sincronização Olá é compartilhada entre todos os agentes de saudação. No entanto, apenas um desses agentes pode ter o serviço do servidor multi-Factor Auth hello está em execução. Esta guia permite que você tooselect Olá servidor multi-Factor Auth que deve ser habilitado para sincronização.

![Servidores Multi-Factor Auth](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
