---
title: "Sincronização do Azure AD Connect: Compreendendo a configuração padrão da saudação | Microsoft Docs"
description: "Este artigo descreve a configuração padrão de saudação na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Sincronização do Azure AD Connect: Compreendendo a configuração padrão da saudação
Este artigo explica as regras de configuração fora da caixa de saudação. Ele documenta regras hello e como essas regras afetam a configuração de saudação. Também lhe orienta pela configuração de padrão de saudação de sincronização do Azure AD Connect. meta de saudação é que o leitor Olá entenda como o modelo de configuração de hello, chamado provisionamento declarativo, está trabalhando em um exemplo do mundo real. Este artigo pressupõe que você já instalou e configura a sincronização do Azure AD Connect usando o Assistente de instalação de saudação.

detalhes do toounderstand Olá Olá do modelo de configuração, ler [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Regras de fora da caixa de tooAzure local AD
Olá expressões a seguir podem ser encontradas na configuração do hello fora da caixa.

### <a name="user-out-of-box-rules"></a>Regras prontas para uso do usuário
Essas regras também se aplicam a tipo de objeto iNetOrgPerson toohello.

Um objeto de usuário deve atender Olá toobe sincronizado a seguir:

* Deve ter um sourceAnchor.
* Depois de saudação objeto foi criado no AD do Azure e sourceAnchor não é possível alterar. Se o valor de saudação é alterada no local, objeto Olá para sincronizando até que Olá sourceAnchor é alterado valor anterior tooits voltar.
* Deve ter Olá accountEnabled (userAccountControl) atributo preenchido. Com um local no Active Directory, esse atributo sempre está presente e preenchido.

Olá seguintes objetos de usuário é **não** sincronizados tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Certifique-se de muitos objetos fora da caixa no Active Directory, como a conta de administrador interno hello, não estão sincronizados.
* `IsPresent([sAMAccountName]) = False`. Certifique-se de que os objetos de usuário sem o atributo sAMAccountName não estejam sincronizados. Esse caso ocorre na prática apenas em um domínio atualizado do NT4.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Não sincronize a conta de serviço de saudação usada pela sincronização do Azure AD Connect e suas versões anteriores.
* Não sincronize contas do Exchange que não funcionem no Exchange Online.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Não sincronize objetos que não funcionem no Exchange Online.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Máscara de bit (& H21C07000) seriam filtrar Olá seguintes objetos:
  * Pasta pública habilitada para email
  * Caixa de correio do Atendedor do sistema
  * Caixa de correio do banco de dados de correio (caixa de correio do sistema)
  * Grupo de segurança universal (não se aplica a um usuário, mas está presente por motivos herdados)
  * Grupo não universal (não se aplica a um usuário, mas está presente por motivos herdados)
  * Plano de caixa de correio
  * Caixa de correio de descoberta
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Não sincronize nenhum objetos vítima de replicação.

Olá regras de atributos a seguir se aplicam:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. atributo sourceAnchor de saudação não vêm de uma caixa de correio vinculada. Presume-se que, se uma caixa de correio vinculada foi encontrada, conta real Olá é associada posteriormente.
* Exchange relacionados os atributos são sincronizados apenas se hello atributo **mailNickName** tem um valor.
* Quando há várias florestas, atributos são consumidos no hello ordem a seguir:
  1. Atributos relacionados na toosign (por exemplo userPrincipalName) são a contribuição da floresta Olá com uma conta ativada.
  2. Atributos que podem ser encontrados em um GAL (lista de endereços Global) do Exchange são a contribuição da floresta Olá com uma caixa de correio do Exchange.
  3. Se não for possível localizar nenhuma caixa de correio, esses atributos poderão vir de qualquer floresta.
  4. Exchange relacionados a atributos (atributos técnicos não é visíveis no hello GAL) são a contribuição da floresta Olá onde `mailNickname ISNOTNULL`.
  5. Se houver várias florestas que seriam satisfazer uma dessas regras, em seguida, Olá (data/hora) de ordem de criação de conectores hello (florestas) é usado toodetermine qual floresta contribui atributos hello.

### <a name="contact-out-of-box-rules"></a>Regras prontas para uso de contato
Um objeto de contato deve satisfazer Olá toobe sincronizado a seguir:

* Contate o Hello deve estar habilitado para email. Ela é verificada com hello regras a seguir:
  * `IsPresent([proxyAddresses]) = True)`. atributo proxyAddresses de saudação deve ser preenchido.
  * Um endereço de email primário pode ser encontrado no atributo proxyAddresses de saudação ou atributo de mensagem de saudação. Olá a presença de um @ é usado tooverify conteúdo Olá é um endereço de email. Uma dessas duas regras deve ser avaliado tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. Há uma entrada com "SMTP:" e, se houver, pode um @ foi encontrada na cadeia de caracteres hello?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. É Olá populado de atributo de email e, se for, pode um @ foi encontrada na cadeia de caracteres hello?

Olá seguintes objetos de contato é **não** sincronizados tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Certifique-se de que nenhum objeto de contato marcado como crítico seja sincronizado. Não deve ser nenhum com uma configuração padrão.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Esses objetos não funcionam no Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Não sincronize nenhum objetos vítima de replicação.

### <a name="group-out-of-box-rules"></a>Grupo prontas para uso de grupo
Um objeto de grupo deve satisfazer Olá toobe sincronizado a seguir:

* Deve ter menos de 50 mil membros. Essa contagem é o número de saudação de membros no grupo local de saudação.
  * Se ela tiver mais membros antes do início da sincronização Olá primeira vez, o grupo de saudação não está sincronizado.
  * Se o número Olá de membros aumentam de quando ele foi inicialmente criado, em seguida, quando chega a 50.000 membros, que ele será interrompido até que a contagem de associação de saudação é menor que 50.000 novamente a sincronização.
  * Observação: a contagem de associação 50.000 Olá também é imposta pelo AD do Azure. Você não é toosynchronize capaz de grupos com mais membros do mesmo se você modifica ou remove essa regra.
* Se o grupo de saudação for um **grupo de distribuição**, em seguida, ele também deve ser habilitado para email. Consulte [Regras prontas para uso de contato](#contact-out-of-box-rules) para ver como essa regra é aplicada.

Olá seguintes objetos de grupo é **não** sincronizados tooAzure AD:

* `IsPresent([isCriticalSystemObject])`. Certifique-se de muitos objetos fora da caixa no Active Directory, como o grupo de administradores internos hello, não estão sincronizados.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Grupo herdado usado pelo DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Grupo de funções.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Não sincronize nenhum objetos vítima de replicação.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>Regras prontas para uso de ForeignSecurityPrincipal
FSPs são unidas muito "qualquer" (\*) objeto no metaverso hello. Na verdade, essa junção ocorre apenas para usuários e grupos de segurança. Essa configuração garante que as associações entre florestas sejam resolvidas e representadas corretamente no Azure AD.

### <a name="computer-out-of-box-rules"></a>Regras prontas para uso de computador
Um objeto de computador deve atender Olá toobe sincronizado a seguir:

* `userCertificate ISNOTNULL`. Somente os computadores Windows 10 populam esse atributo. Todos os objetos de computador com um valor nesse atributo serão sincronizados.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Noções básicas sobre o cenário de regras prontas de saudação
Neste exemplo, estamos usando uma implantação com uma floresta de contas (A), uma floresta de recursos (R) e um diretório do Azure AD.

![Imagem com a descrição do cenário](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

Nessa configuração, presume-se que houver uma conta ativada na floresta de conta hello e uma conta desativada na floresta de recursos de saudação com uma caixa de correio vinculada.

Nosso objetivo com a configuração padrão de saudação é:

* Atributos relacionados na toosign serão sincronizados com a floresta de saudação com conta Olá habilitado.
* Atributos que podem ser encontrados no hello GAL (lista de endereços Global) são sincronizados de floresta Olá com caixa de correio hello. Se nenhuma caixa de correio for encontrada, nenhuma outra floresta será usada.
* Se uma caixa de correio vinculada for encontrada, hello conta habilitada vinculada deve ser encontrada para Olá objeto toobe exportado tooAzure AD.

### <a name="synchronization-rule-editor"></a>Editor de Regra de Sincronização
configuração Olá pode ser exibida e alterada com a ferramenta de saudação Editor de regras de sincronização (SRE) e pode ser encontrado tooit um atalho no menu de início de saudação.

![Ícone do Editor de Regras de Sincronização](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Olá SRE é uma ferramenta do kit de recursos e é instalado com a sincronização do Azure AD Connect. toostart capaz de toobe-lo, você deve ser um membro do grupo ADSyncAdmins de saudação. Quando ele é iniciado, você vê algo assim:

![Regras de Sincronização Entrada](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Nesse painel, você vê todas as regras de sincronização criadas para sua configuração. Cada linha na tabela de saudação é uma regra de sincronização. toohello à esquerda em tipos de regra, Olá dois tipos diferentes estão listados: entrada e saída. Entrada e saída é da exibição de saudação do metaverso hello. São principalmente contínuo toofocus em Olá regras nesta visão geral de entrada. lista real de saudação de regras de sincronização depende do esquema Olá detectado no AD. Imagem de saudação acima, conta de saudação floresta (fabrikamonline.com) não tem todos os serviços, como o Exchange e Lync e não há regras de sincronização ter sido criada para esses serviços. No entanto, na floresta de recursos da saudação (res.fabrikamonline.com) encontrar regras de sincronização para esses serviços. Olá conteúdo regras Olá é diferente dependendo da versão de hello detectada. Por exemplo, em uma implantação com o Exchange 2013, há mais fluxos de atributo configurados do que no Exchange 2010/2007.

### <a name="synchronization-rule"></a>Regra de Sincronização
Uma regra de sincronização é um objeto de configuração com um conjunto de atributos que fluem quando uma condição é atendida. Também é usado toodescribe como um objeto em um espaço do conector é objeto tooan relacionados no metaverso hello, conhecido como **junção** ou **corresponder**. Regras de sincronização Olá ter um valor de precedência como elas se relacionam tooeach outros. Uma regra de sincronização com um valor numérico mais baixo tem precedência maior e em um conflito de fluxo de atributo, wins de maior precedência Olá resolução de conflitos.

Por exemplo, examinar Olá regra de sincronização **no AD – usuário AccountEnabled**. Marcar esta linha hello SRE e selecione **editar**.

Desde que esta regra é uma regra de caixa de saída, você receberá um aviso quando você abre a regra de saudação. Você não deve fazer qualquer [altera as regras de caixa de tooout](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), portanto, você será solicitado a quais são suas intenções. Nesse caso, você deseja apenas tooview regra de saudação. Selecione **Não**.

![Aviso de Regras de Sincronização](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Uma Regra de Sincronização tem quatro seções de configuração: descrição, filtro de escopo, regras de associação e transformações.

#### <a name="description"></a>Descrição
primeira seção do Hello fornece informações básicas, como um nome e uma descrição.

![Guia Descrição no Editor de regras de sincronização ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

Você também encontrar informações sobre qual sistema conectado essa regra está relacionada, que tipo de saudação do objeto conectado system aplica-se a e Olá o tipo de objeto do metaverso. tipo de objeto do metaverso Olá é sempre pessoa, independente de quando o tipo de objeto de fonte de saudação é um usuário, iNetOrgPerson ou contato. tipo de objeto do metaverso Olá nunca deve alterar para que ele é criado como um tipo genérico. saudação de tipo de Link pode ser definida tooJoin, StickyJoin ou provisão. Essa configuração funciona junto com a seção de regras de união hello e é abordada posteriormente.

Você também pode ver que essa regra de sincronização é usada para a sincronização de senha. Se um usuário estiver no escopo para essa regra de sincronização, senha Olá é sincronizada entre locais toocloud (supondo que você habilitou o recurso de sincronização de senha Olá).

#### <a name="scoping-filter"></a>Filtro de escopo
Olá seção filtro de escopo é tooconfigure usado quando uma regra de sincronização deve ser aplicada. Como o nome de saudação do hello regra de sincronização que você está observando indica que deve ser aplicada apenas para usuários habilitados, o escopo de saudação é configurado caso atributo de saudação AD **userAccountControl** deve não ter Olá conjunto de bits de 2. Quando o mecanismo de sincronização de saudação localiza um usuário no AD, ele se aplica a esta sincronização regra quando **userAccountControl** é definir o valor decimal de toohello 512 (usuário normal ativado). Regra de saudação não é aplicável quando o usuário Olá tem **userAccountControl** definir too514 (usuário normal desativado).

![Guia Escopo no Editor de regras de sincronização ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

filtro de escopo de saudação possui grupos e cláusulas que podem ser aninhadas. Todas as cláusulas dentro de um grupo devem ser satisfeitas para uma regra de sincronização tooapply. Quando vários grupos são definidos, pelo menos um grupo deve ser atendido para Olá regra tooapply. Ou seja, um OR lógico é avaliado entre grupos e um AND lógico é avaliado dentro de um grupo. Um exemplo dessa configuração pode ser encontrado no hello regra de sincronização de saída **Out tooAAD – Group Join**. Há vários grupos de filtro de sincronização, por exemplo, um para grupos de segurança (`securityEnabled EQUAL True`) e outro para grupos de distribuição (`securityEnabled EQUAL False`).

![Guia Escopo no Editor de regras de sincronização ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Essa regra é usada toodefine quais grupos devem ser provisionado tooAzure AD. Grupos de distribuição devem ser habilitado para email toobe sincronizado com o AD do Azure, mas um email para grupos de segurança não é necessário.

#### <a name="join-rules"></a>Regras de associação
seção terceira Olá é tooconfigure usada como objetos no espaço do conector Olá se relacionam tooobjects no metaverso hello. Olá regra que procuramos anteriormente não tem qualquer configuração de regras de união, portanto em vez disso, você está indo toolook em **no AD – usuário Join**.

![Guia Regras de junção no Editor de regras de sincronização ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

conteúdo de saudação da regra de associação Olá depende Olá correspondência opção selecionada no Assistente de instalação de saudação. Para uma regra de entrada, avaliação Olá inicia com um objeto no espaço do conector de origem hello e cada grupo de regras de junção Olá é avaliado em sequência. Se um objeto de origem é avaliado toomatch exatamente um objeto em Olá metaverso usando uma das regras de junção hello, objetos de saudação são Unidos. Se todas as regras foram avaliadas e não há nenhuma correspondência, Olá tipo de Link na página de descrição de saudação é usado. Se essa configuração for definida muito**provisionar**, em seguida, um novo objeto é criado no destino hello, Olá metaverso. tooprovision um novo metaverso de toohello de objeto também é conhecido como muito**projeto** metaverso de toohello um objeto.

regras de união Olá são avaliadas somente uma vez. Quando um objeto de espaço do conector e um objeto do metaverso são Unidos, eles permanecem Unidos como escopo Olá Olá regra de sincronização for atendido.

Ao serem avaliadas Regras de Sincronização, apenas uma Regra de Sincronização com as regras de associação definidas deve estar no escopo. Se forem encontradas várias Regras de Sincronização com regras de associação para um objeto, um erro será gerado. Por esse motivo, a prática recomendada de saudação é toohave somente uma regra de sincronização com junção definida quando várias regras de sincronização estão no escopo de um objeto. Na configuração de fora da caixa de saudação para sincronização do Azure AD Connect, essas regras podem ser encontrados examinando o nome de saudação e encontrá-las com a palavra hello **ingressar** final de saudação do nome de saudação. Uma regra de sincronização sem nenhuma regra de associação definida se aplica a fluxos de atributo hello quando outra regra de sincronização unidas objetos hello ou provisionou um novo objeto no destino hello.

Se você observar a imagem de saudação acima, você pode ver a regra hello está tentando toojoin **objectSID** com **msExchMasterAccountSid** (Exchange) e **msRTCSIP OriginatorSid** ( Lync), que é o esperado em uma topologia de floresta de conta-recurso. Localize Olá mesma regra em todas as florestas. Olá pressupõe-se que cada floresta pode ser uma conta ou um recurso de floresta. Essa configuração também funcionará se você tiver contas que residem em uma única floresta e não tem toobe associado.

#### <a name="transformations"></a>Transformações
Olá seção sobre transformação define todos os fluxos de atributos que se aplicam a objeto de destino toohello quando objetos de saudação são Unidos e filtro de escopo de saudação for atendido. Voltando toohello **no AD – usuário AccountEnabled** regra de sincronização, você encontrar hello transformações a seguir:

![Guia Transformações no Editor de regras de sincronização ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput essa configuração no contexto em uma implantação de floresta de conta-recurso, é esperado toofind uma conta ativada na floresta de conta hello e uma conta desabilitada no recurso Olá floresta com as configurações do Exchange e Lync. Olá regra de sincronização que você está observando contém atributos de saudação necessários para entrar e esses atributos devem fluir de floresta Olá onde há uma conta habilitada. Todos esses fluxos de atributo são colocados juntos em uma Regra de Sincronização.

Uma transformação pode ter diferentes tipos: constante, direta e expressão.

* Um fluxo constante sempre flui um valor codificado. No caso de Olá acima, ele sempre define o valor de saudação **True** no atributo do metaverso Olá chamado **accountEnabled**.
* Um fluxo direto sempre fluxos de valor de saudação do atributo de saudação no atributo de destino do hello origem toohello como-é.
* tipo de fluxo Olá terceiro é a expressão e permite configurações mais avançadas.

linguagem de expressão Olá é VBA (Visual Basic for Applications), portanto as pessoas com experiência em Microsoft Office ou VBScript reconhecerão o formato de saudação. Os atributos são colocados entre colchetes, [attributeName]. Nomes de função e nomes de atributo diferenciam maiusculas de minúsculas, mas hello Editor de regras de sincronização avalia as expressões de saudação e fornecerá um aviso se a expressão de saudação não é válida. Todas as expressões são expressas em uma única linha com funções aninhadas. alimentação de saudação tooshow da linguagem de configuração Olá, aqui é Olá fluxo para pwdLastSet, mas com comentários adicionais inseridos:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Consulte [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) para obter mais informações sobre a linguagem de expressão Olá para fluxos de atributo.

### <a name="precedence"></a>Precedência
Você vimos agora algumas regras de sincronização individuais, mas as regras de saudação trabalham juntas na configuração de saudação. Em alguns casos, um valor de atributo vêm de várias toohello de regras de sincronização mesmo atributo de destino. Nesse caso, a precedência de atributo é usado toodetermine qual atributo wins. Por exemplo, examine Olá atributo sourceAnchor. Esse atributo é um toosign possível do atributo importante toobe em tooAzure AD. Você pode encontrar um fluxo de atributo para esse atributo em duas diferentes regras de sincronização, **Entrada do AD – usuário AccountEnabled** e **Entrada do AD – usuário comum**. Devido a precedência de regra tooSynchronization, atributo de sourceAnchor Olá vêm de floresta Olá com uma conta ativada primeiro quando há vários objetos Unidos toohello metaverso object. Se não há contas habilitado, usos de mecanismo de sincronização Olá Olá regra de sincronização de capturar todos **no AD – usuário Common**. Essa configuração garante que, até mesmo para contas desabilitadas, ainda haja um sourceAnchor.

![Regras de Sincronização Entrada](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

precedência de saudação para regras de sincronização é definida em grupos pelo Assistente de instalação de saudação. Saudação de ter todas as regras em um grupo de mesmo nome, mas eles são diretórios conectados toodifferent conectado. Assistente de instalação Olá fornece regra Olá **no AD – usuário Join** precedência mais alta e ele itera todos os diretórios conectados do AD. Ele continuará com grupos de Avançar Olá de regras em uma ordem predefinida. Dentro de um grupo, são adicionadas regras Olá Olá Olá de ordem que conectores foram adicionados no Assistente de saudação. Se outro conector for adicionado por meio do Assistente de saudação, Olá regras de sincronização serão reordenadas e regras do hello novo conector são inseridas por último em cada grupo.

### <a name="putting-it-all-together"></a>Juntando as peças
Já sabemos o suficiente sobre regras de sincronização toobe capaz de toounderstand, como configuração Olá funciona com hello diferentes regras de sincronização. Se você observar um usuário e Olá atributos que são contribuíram toohello metaverso, Olá regras são aplicadas na ordem de saudação:

| Nome | Comentário |
|:--- |:--- |
| Entrada do AD – Associação de Usuário |Regra para associar objetos de espaço conector com metaverso. |
| Entrada do AD – UserAccount habilitada |Atributos necessários para entrar tooAzure AD e Office 365. Queremos estes atributos da conta de saudação habilitada. |
| Entrada do AD – usuário comum do Exchange |Atributos encontrados na lista de endereços Global de saudação. Vamos supor que Olá qualidade dos dados é melhor na floresta Olá onde encontramos a caixa de correio do usuário hello. |
| Entrada do AD – usuário comum |Atributos encontrados na lista de endereços Global de saudação. No caso de não encontrarmos uma caixa de correio, qualquer outro objeto Unido pode contribuir valor do atributo hello. |
| Entrada do AD – usuário do Exchange |Existe somente se o Exchange foi detectado. Flui todos os atributos do Exchange de infraestrutura. |
| Entrada do AD – usuário Lync |Existe somente se o Lync foi detectado. Flui todos os atributos do Lync de infraestrutura. |

## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre o modelo de configuração de saudação em [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Leia mais sobre a linguagem de expressão Olá em [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Continuar a ler como configuração de out-of-box Olá funciona no [Noções básicas sobre usuários e contatos](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Veja como toomake um práticos alterados usando provisionamento declarativo em [como toomake toohello uma alteração de configuração padrão](active-directory-aadconnectsync-change-the-configuration.md).

**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

