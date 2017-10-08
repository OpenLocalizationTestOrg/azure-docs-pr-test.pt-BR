---
title: 'Azure AD Connect: conceitos de design | Microsoft Docs'
description: "Este tópico detalha determinadas áreas de design da implementação"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: conceitos de design
Olá finalidade deste tópico é toodescribe áreas que devem ser consideradas por meio de durante o design de implementação de saudação do Azure AD Connect. Este tópico é um aprofundamento em determinadas áreas e esses conceitos também são descritos brevemente em outros tópicos.

## <a name="sourceanchor"></a>sourceAnchor
atributo sourceAnchor de saudação é definido como *um atributo imutável durante o tempo de vida de saudação de um objeto*. Identifica exclusivamente um objeto como sendo Olá mesmo local do objeto e no AD do Azure. também é chamado de atributo Olá **immutableId** e nomes de saudação dois são usados intercambiáveis.

palavra de saudação imutável, que é "não pode ser alterado", é importante toothis tópico. Como valor do atributo não pode ser alterado depois que ele tiver sido definido, é importante toopick um design que dá suporte ao seu cenário.

Olá atributo é usado para Olá os seguintes cenários:

* Quando um novo servidor de mecanismo de sincronização é compilado ou recompilado após um cenário de recuperação de desastre, esse atributo vincula objetos existentes no Azure AD a objetos locais.
* Se você mover de um modelo de identidade sincronizado tooa identidade somente em nuvem, este atributo permite que os objetos muito "correspondência rígido" objetos existentes no AD do Azure com objetos locais.
* Se você usar a federação, em seguida, esse atributo junto com hello **userPrincipalName** é usado em Olá declaração toouniquely identificar um usuário.

Este tópico trata apenas sourceAnchor toousers relacionado. Hello mesmas regras se aplicam tooall tipos de objeto, mas é apenas para os usuários que geralmente, esse problema é uma preocupação.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Selecionando um bom atributo sourceAnchor
o valor do atributo Olá deve seguir Olá regras a seguir:

* Ter menos de 60 caracteres
  * Caracteres diferentes de a-z, A-Z ou 0-9 são codificados e contados como 3 caracteres
* Não conter nenhum caractere especial: &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Ser globalmente exclusivo
* Ser uma cadeia de caracteres, um inteiro ou um binário
* Não ser baseado no nome do usuário, já que isso muda
* Não diferenciar maiúsculas de minúsculas e evitar valores que podem variar maiúsculas e minúsculas
* Deve ser atribuído ao objeto Olá é criado

Se Olá selecionado sourceAnchor não é do tipo cadeia de caracteres, e tooensure de valor de atributo de saudação Base64Encode de se conectar do Azure AD sem caracteres especiais são exibidos. Se você usar outro servidor de federação que o AD FS, verifique se o servidor também pode Base64Encode atributo de saudação.

atributo sourceAnchor de saudação diferencia maiusculas de minúsculas. Um valor de "Lucianasilva" não é Olá igual a "lucianasilva". Porém, você não deve ter dois objetos diferentes com apenas uma diferença de uso de maiúsculas.

Se você tiver uma única floresta local, atributo de hello, em seguida, você deve usar é **objectGUID**. Isso também é atributo Olá usado quando você usa as configurações expressas no Azure AD Connect e também Olá atributo usado pelo DirSync.

Se você tiver várias florestas e não mover os usuários entre florestas e domínios, em seguida, **objectGUID** é uma boa atributo toouse mesmo nesse caso.

Se você mover os usuários entre domínios e florestas, você deve localizar um atributo que não mudam ou pode ser movido com usuários Olá durante saudação movimentação. Uma abordagem recomendada é toointroduce um atributo sintético. Um atributo que contenha algo parecido com um GUID seria adequado. Durante a criação do objeto, um novo GUID é criado e marcado no usuário hello. Uma regra de sincronização personalizadas pode ser criada em toocreate de servidor de mecanismo de sincronização de saudação esse valor com base em Olá **objectGUID** e Olá de atualização de atributo selecionado no ADDS. Quando você move o objeto hello, verifique tooalso-se de copiar o conteúdo de saudação desse valor.

Outra solução é toopick um atributo existente, você sabe que não é alterado. Os atributos usados normalmente incluem **employeeID**. Se você considerar um atributo que contém letras, verifique se não há que nenhum caso de Olá chance (letras maiusculas e minúsculas) pode ser alteradas para o valor do atributo hello. Atributos inválidos que não devem ser usados incluem os atributos com o nome de saudação do usuário hello. Um casamento ou Divórcio, Olá nome é esperado toochange, que não é permitido para este atributo. Isso também é um motivo por que atributos como **userPrincipalName**, **mail**, e **targetAddress** não são tooselect possível na instalação do hello AD do Azure Connect Assistente. Esses atributos também contêm hello "@" caractere, que não é permitido em Olá sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Atributo sourceAnchor de alteração Olá
valor do atributo sourceAnchor Olá não pode ser alterado depois Olá objeto foi criado no AD do Azure e identity Olá é sincronizado.

Por esse motivo, Olá restrições a seguir se aplicam a tooAzure AD Connect:

* atributo de sourceAnchor Olá só pode ser definido durante a instalação inicial. Se você executar novamente o Assistente de instalação hello, essa opção é somente leitura. Se você precisar toochange essa configuração, você deve desinstalar e reinstalar.
* Se você instalar outro servidor do Azure AD Connect, em seguida, você deve selecionar Olá mesmo atributo sourceAnchor usado anteriormente. Se anteriormente tiver sido usando o DirSync e mover tooAzure AD conectar-se de que, em seguida, você deve usar **objectGUID** já que esse é o atributo de saudação usado pelo DirSync.
* Se Olá valor sourceAnchor é alterado após o objeto de saudação foi exportado tooAzure AD, depois do Azure AD Connect sincronização gera um erro e não permite mais alterações no objeto antes de saudação problema foi corrigido e Olá sourceAnchor é alterado em Olá diretório de origem.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Usando o msDS-ConsistencyGuid como sourceAnchor
Por padrão, o Azure AD Connect (versão 1.1.486.0 e anteriores) usa o objectGUID como atributo de sourceAnchor hello. O ObjectGUID é gerado pelo sistema. Não é possível especificar seu valor ao criar objetos do AD locais. Como explicado na seção [sourceAnchor](#sourceanchor), há cenários em que você precisa que o valor de sourceAnchor toospecify hello. Se cenários Olá tooyou aplicável, você deve usar um atributo do AD (por exemplo, msDS-ConsistencyGuid) podem ser configurado como atributo de sourceAnchor hello.

Conexão do AD do Azure (versão 1.1.524.0 e posterior) agora facilita o uso de saudação do msDS-ConsistencyGuid como o atributo sourceAnchor. Ao usar esse recurso, o Azure AD Connect configura automaticamente regras de sincronização Olá para:

1. Use msDS-ConsistencyGuid como atributo de sourceAnchor Olá para objetos de usuário. O ObjectGUID é usado para outros tipos de objeto.

2. Para qualquer local AD usuário cujo atributo msDS-ConsistencyGuid não está preenchido, o Azure AD Connect grava seu atributo de msDS-ConsistencyGuid toohello back objectGUID valor no Active Directory no local do objeto. Depois que o atributo msDS-ConsistencyGuid de saudação for preenchido, Azure AD Connect, em seguida, exporta Olá objeto tooAzure AD.

>[!NOTE]
> Uma vez um local em objeto do AD é importado para o Azure AD Connect (isto é, importado para Olá espaço do conector AD e projetado em Olá metaverso), você não pode alterar seu valor sourceAnchor mais. valor de sourceAnchor toospecify Olá para um dado local AD de objeto, defina o atributo msDS-ConsistencyGuid antes de ele ser importado para o Azure AD Connect.

### <a name="permission-required"></a>Permissão necessária
Para esse recurso toowork, Olá AD DS conta usada toosynchronize com o Active Directory no local deve ser concedida gravação permissão toohello msDS-ConsistencyGuid atributo no Active Directory no local.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Como tooenable Olá ConsistencyGuid recurso - nova instalação
Você pode habilitar o uso de saudação do ConsistencyGuid como sourceAnchor durante a instalação de novo. Esta seção aborda tanto a instalação Expressa quanto a Personalizada em detalhes.

  >[!NOTE]
  > Somente as versões mais recentes do Azure AD Connect (1.1.524.0 e posterior) dá suporte a Olá uso de ConsistencyGuid como sourceAnchor durante a instalação de novo.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Como tooenable Olá ConsistencyGuid recurso
No momento, o recurso de Olá só pode ser habilitado durante a nova instalação do Azure AD Connect somente.

#### <a name="express-installation"></a>Instalação Expressa
Durante a instalação do Azure AD Connect com o modo expresso, o Assistente de conexão do AD do Azure Olá determina automaticamente Olá anúncio mais apropriado atributo toouse como atributo de sourceAnchor hello usando Olá lógica a seguir:

* Primeiro, consultas de assistente conectar de saudação do AD do Azure que seu atributo do AD do Azure locatário tooretrieve Olá AD usado como Olá atributo sourceAnchor na instalação do hello anterior do Azure AD Connect (se houver). Se essas informações estão disponíveis, o Azure AD Connect usa o atributo de saudação mesmo AD.

  >[!NOTE]
  > Somente as versões mais recentes do Azure AD Connect (1.1.524.0 e depois) armazena informações em seu locatário do AD do Azure sobre o atributo sourceAnchor de saudação usado durante a instalação. Versões mais antigas do Azure AD Connect não fazem isso.

* Se informações sobre Olá sourceAnchor atributo usado não estiverem disponíveis, o Assistente de saudação verifica estado de saudação do atributo de msDS-ConsistencyGuid Olá no Active Directory local. Se o atributo de saudação não está configurado em qualquer objeto no diretório Olá, o Assistente de Olá usa Olá msDS-ConsistencyGuid como atributo de sourceAnchor hello. Se o atributo Olá estiver configurado em um ou mais objetos no diretório hello, Assistente de saudação conclui atributo hello está sendo usado por outros aplicativos e não é adequado como atributo sourceAnchor...

* Nesse caso, Assistente de saudação reverterá toousing objectGUID como atributo de sourceAnchor hello.

* Depois que o atributo sourceAnchor de saudação é decidido, o assistente Olá armazena informações de saudação em seu locatário do AD do Azure. Olá informações serão usadas pela instalação futuras do Azure AD Connect.

Após a conclusão da instalação do Express, o assistente Olá informa separado qual atributo como atributo de âncora de origem de saudação.

![O assistente informa qual atributo do AD foi escolhido como sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Instalação personalizada
Ao instalar o Azure AD Connect com modo personalizado, o Assistente de conexão do AD do Azure Olá fornece duas opções ao configurar o atributo sourceAnchor:

![Instalação personalizada – configuração do sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Configuração | Descrição |
| --- | --- |
| Permitir que o Azure gerenciar âncora de origem Olá para mim | Selecione esta opção se você quiser o atributo do AD do Azure toopick Olá para você. Se você selecionar essa opção, o Azure AD Connect assistente aplica Olá mesmo [lógica de seleção do atributo sourceAnchor usada durante a instalação do Express](#express-installation). Instalação tooExpress semelhante, o Assistente de saudação informa qual atributo separado como Olá atributo de âncora de origem após a conclusão da instalação personalizada. |
| Um atributo específico | Selecione esta opção se desejar toospecify um atributo de AD existente como Olá sourceAnchor. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Como tooenable Olá ConsistencyGuid recurso - implantação existente
Se você tiver uma implantação existente do Azure AD Connect, que está usando o objectGUID como atributo de âncora de origem hello, você pode desativá-toousing ConsistencyGuid em vez disso.

>[!NOTE]
> Somente as versões mais recentes do Azure AD Connect (1.1.552.0 e posterior) dá suporte à alternância de tooConsistencyGuid ObjectGuid como atributo de âncora de origem de saudação.

tooswitch de tooConsistencyGuid objectGUID como atributo de âncora de origem hello:

1. Iniciar Assistente para conectar-se de saudação do AD do Azure e clique em **configurar** tela de tarefas toohello toogo.

2. Selecione Olá **configurar âncora de origem** opção de tarefas e clique em **próximo**.

   ![Habilitar ConsistencyGuid para implantação existente – etapa 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Insira suas credenciais de administrador do Azure AD e clique em **Avançar**.

4. Assistente de conexão do AD do Azure analisa o estado de saudação do atributo de msDS-ConsistencyGuid Olá no Active Directory local. Se o atributo de saudação não está configurado em qualquer objeto em Olá que diretório, o Azure AD Connect conclui que nenhum outro aplicativo está usando atualmente o atributo hello e é seguro toouse-lo como atributo de âncora de origem hello. Clique em **próximo** toocontinue.

   ![Habilitar ConsistencyGuid para implantação existente – etapa 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. Em Olá **tooConfigure pronto** tela, clique em **configurar** toomake alteração de configuração de saudação.

   ![Habilitar ConsistencyGuid para implantação existente – etapa 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Após a conclusão da configuração hello, o Assistente de saudação indica que msDS-ConsistencyGuid agora está sendo usada como atributo de âncora de origem hello.

   ![Habilitar ConsistencyGuid para implantação existente – etapa 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Durante a análise da saudação (etapa 4), se o atributo de saudação é configurado em um ou mais objetos no diretório Olá, Assistente de saudação conclui atributo hello está sendo usado por outro aplicativo e retorna um erro, como ilustrado no diagrama de saudação abaixo. Se você tem certeza de que o atributo Olá não é usado por aplicativos existentes, será necessário toocontact suporte para obter informações sobre como toosuppress Olá erro.

![Habilitar ConsistencyGuid para implantação existente – erro](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Impacto sobre o AD FS ou a configuração de federação de terceiros
Se você estiver usando o Azure AD Connect toomanage de implantação do AD FS no local, Olá do Azure AD Connect atualiza automaticamente Olá regras toouse Olá AD mesmo atributo de declaração de como sourceAnchor. Isso garante que essa declaração de ImmutableID Olá gerada pelo AD FS é consistente com hello sourceAnchor valores exportados tooAzure AD.

Se você estiver gerenciando o AD FS fora do Azure AD Connect ou você estiver usando servidores de federação de terceiros para autenticação, você deve atualizar manualmente as regras de declaração Olá para ImmutableID declaração toobe consistente com os valores de sourceAnchor hello exportada tooAzure AD como descrito na seção do artigo [regras de declaração de modificar o AD FS](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Assistente de saudação retorna Olá aviso a seguir após a conclusão da instalação:

![Configuração da federação de terceiros](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Adicionar nova implantação de tooexisting de diretórios
Suponha que você implantou o Azure AD Connect com hello ConsistencyGuid recurso habilitado, e agora deseja tooadd outra implantação de toohello do diretório. Quando você tenta tooadd diretório de hello, Assistente do Azure AD Connect verifica estado de saudação do atributo de mSDS-ConsistencyGuid Olá no diretório de saudação. Se o atributo Olá estiver configurado em um ou mais objetos no diretório hello, Assistente de saudação conclui atributo hello está sendo usado por outros aplicativos e retorna um erro, como ilustrado no diagrama de saudação abaixo. Se você tem certeza de que o atributo Olá não é usado por aplicativos existentes, será necessário toocontact suporte para obter informações sobre como toosuppress Olá erro.

![Adicionar nova implantação de tooexisting de diretórios](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Entrar no Azure AD
Ao integrar seu diretório local com o Azure AD, é importante toounderstand como as configurações de sincronização de saudação podem afetar o usuário de maneira Olá autentica. AD do Azure usa o usuário de saudação tooauthenticate userPrincipalName (UPN). No entanto, quando você sincroniza os usuários, você deve escolher Olá atributo toobe utilizada para valor de userPrincipalName cuidadosamente.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Escolher o atributo userPrincipalName Olá
Quando você seleciona atributo Olá para fornecer o valor de saudação do UPN toobe usado no Azure deve verificar

* toohello UPN sintaxe (RFC 822), que ele deve ter o formato de saudação está de acordo com os valores de atributo Oláusername@domain
* sufixo Olá Olá valores correspondências tooone de saudação verificado domínios personalizados no AD do Azure

Em configurações expressas, Olá assumido escolha para atributo Olá é userPrincipalName. Se o atributo userPrincipalName de saudação não contém um valor de saudação desejado toosign seus usuários em tooAzure, você deve escolher **instalação personalizada**.

### <a name="custom-domain-state-and-upn"></a>Estado de domínio personalizado e UPN
É importante tooensure que há um domínio verificado para o sufixo UPN hello.

John é um usuário em contoso.com. Você deseja John toouse Olá UPN local john@contoso.com toosign em tooAzure após foram sincronizadas usuários tooyour AD do Azure diretório contoso.onmicrosoft.com. toodo assim, você precisa tooadd e verifique se o contoso.com como um domínio personalizado no AD do Azure antes de começar sincronizar usuários hello. Se o sufixo UPN Olá John, por exemplo, contoso.com, não coincide com um domínio verificado no AD do Azure, o AD do Azure substitui sufixo UPN Olá com contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Domínios locais não roteáveis e UPN para Azure AD
Algumas organizações têm domínios não roteáveis, como contoso.local ou domínios de rótulo único simples, como contoso. Você não é capaz de tooverify um domínio não roteável no AD do Azure. Conexão do AD do Azure pode sincronizar tooonly um domínio verificado no AD do Azure. Quando você cria um diretório do Azure AD, ele cria um domínio roteável que torna-se o domínio padrão do Azure AD, por exemplo, contoso.onmicrosoft.com. Portanto, é necessário tooverify qualquer outro domínio roteável nesse cenário caso você não deseje toosync toohello padrão onmicrosoft.com domínio.

Leitura [adicionar seu nome de domínio personalizado tooAzure do Active Directory](../active-directory-add-domain.md) para obter mais informações sobre como adicionar e verificar os domínios.

O Azure AD Connect detecta se você está executando em um ambiente de domínio não roteável e avisa corretamente para não prosseguir com configurações expressas. Se você estiver operando em um domínio não pode ser roteado, em seguida, é provável que UPN de usuários Olá Olá ter muito sufixos não roteável. Por exemplo, se você estiver executando em contoso. local, o Azure AD Connect sugere você toouse configurações personalizadas em vez de usar configurações expressas. Usando configurações personalizadas, você está toospecify capaz de atributo de saudação que deve ser usado como o UPN toosign em tooAzure depois usuários Olá são sincronizado tooAzure AD.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
