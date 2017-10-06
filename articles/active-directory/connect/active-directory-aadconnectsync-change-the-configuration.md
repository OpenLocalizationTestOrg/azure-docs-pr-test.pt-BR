---
title: "Azure AD Connect: alterar uma configuração na sincronização do Azure AD Connect | Microsoft Docs"
description: "Explica como toomake toohello uma alteração da configuração no Azure AD Connect sincronizar."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Sincronização do Azure AD Connect: como toomake toohello uma alteração de configuração padrão
Olá finalidade deste tópico é toowalk você por meio de como toomake altera a configuração padrão de toohello na sincronização do Azure AD Connect. Ele fornece etapas para alguns cenários comuns. Com esse conhecimento, você deve ser capaz de toomake tooyour algumas alterações simples possui configuração com base em regras de negócios.

## <a name="synchronization-rules-editor"></a>Editor de Regras de Sincronização
Olá Editor de regras de sincronização é a configuração de padrão de saudação usada de toosee e alteração. Você pode encontrar no hello Menu Iniciar em Olá **do Azure AD Connect** grupo.  
![Menu Iniciar com o Editor de Regras de Sincronização](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Quando você abri-lo, você ver as regras de fora da caixa do saudação padrão.

![Editor de Regras de Sincronização](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Navegando no editor de saudação
Olá listas suspensas na parte superior de saudação do editor de saudação permitem tooquickly localizar uma determinada regra. Por exemplo, se você quiser regras de saudação toosee onde Olá atributo proxyAddresses é incluído, alteraria a seguir Olá suspensas toohello:  
![Filtragem de SRE](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
filtragem de tooreset e carregar uma nova configuração, pressione **F5** teclado hello.

superior toohello direita, você tem um botão **adicionar nova regra**. Esse botão é usado toocreate sua própria regra personalizada.

Na parte inferior do hello, você tem botões para atuar em uma regra de sincronização selecionado. **Editar** e **Excluir** fazem o que você espera. **Exportar** gera um script do PowerShell para recriar a regra de sincronização de saudação. Esse procedimento permite que você toomove uma regra de sincronização de um tooanother de servidor.

## <a name="create-your-first-custom-rule"></a>Criar sua primeira regra personalizada
alteração mais comum de saudação é fluxos de atributo toohello alterações. dados de saudação em seu diretório de origem não podem ser como no AD do Azure. No exemplo hello nesta seção, você deseja toomake se Olá determinado nome de um usuário estará sempre em **maiuscula**.

### <a name="disable-hello-scheduler"></a>Desabilitar o Agendador Olá
Olá [Agendador](active-directory-aadconnectsync-feature-scheduler.md) é executado a cada 30 minutos por padrão. Você deseja toomake-se de que não está sendo iniciada enquanto você estiver fazendo alterações e solucionar problemas de suas regras de novo. tootemporarily desabilitar Olá Agendador, inicie o PowerShell e execute`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Desabilitar o Agendador Olá](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Criar regra de saudação
1. Clique em **Adicionar nova regra**.
2. Em Olá **descrição** entrar na página seguinte hello:  
   ![Filtragem das regras de entrada](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Nome: Dê um nome descritivo de regra de saudação.
   * Descrição: Algum esclarecimento para que outra pessoa possa compreender quais regra Olá destina-se.
   * Sistema conectado: objeto de saudação do sistema Olá pode ser encontrado em. Nesse caso, selecione Olá conector do Active Directory.
   * Tipo de Sistema Conectado/Objeto do Metaverso: selecione **Usuário** e **Pessoa**, respectivamente.
   * Tipo de link: Alterar esse valor também**ingressar**.
   * Precedência: Forneça um valor que seja exclusivo no sistema de saudação. Um valor numérico mais baixo indica uma precedência mais alta.
   * Marcação: deixe em branco. As regras integradas da Microsoft devem ter essa caixa preenchida com um valor.
3. Em Olá **filtro de escopo** insira **givenName ISNOTNULL**.  
   ![Filtrar escopo das regras de entrada](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Esta seção é usada toodefine regra de saudação quais objetos deve ser aplicados a. Se ficar em branco, Olá aplicaria tooall objetos de usuário. Mas isso incluiria as salas de conferência, contas de serviço e outros objetos de usuário que não são de pessoas.
4. Em Olá **regras de junção**, deixe-o vazio.
5. Em Olá **transformações** página, altere Olá FlowType muito**expressão**. Olá selecione atributo de destino **givenName**e na origem insira `PCase([givenName])`.
   ![Transformações das regras de entrada](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   o mecanismo de sincronização Olá diferencia maiusculas de minúsculas tanto no nome da função hello e nome de saudação do atributo hello. Se você digitar algo errado, você ver um aviso quando você adicionar regra de saudação. editor de saudação permite toosave e continuar, portanto, é necessário tooreopen Olá da regra e regra de saudação correto.
6. Clique em **adicionar** toosave regra de saudação.

A nova regra personalizada deve estar visível com hello outra regras de sincronização no sistema de saudação.

### <a name="verify-hello-change"></a>Verifique se a alteração de saudação
Com essa nova alteração, você deseja toomake se ele está funcionando como esperado e não está gerando os erros. Dependendo do número de saudação de objetos que você tem, existem toodo de duas maneiras diferentes esta etapa.

1. Executar uma sincronização completa em todos os objetos
2. Executar uma visualização e uma sincronização completa em um único objeto

Iniciar **serviço de sincronização** saudação do menu de início. etapas de saudação nesta seção estão todos nessa ferramenta.

1. **Sincronização completa em todos os objetos**  
   Selecione **conectores** na parte superior da saudação. Identificar Olá conector que você fez uma seção anterior do alteração tooin hello, nesse caso Olá serviços de domínio do Active Directory e selecioná-lo. Selecione **Executar** em Ações e selecione **Sincronização Completa** e **OK**.
   ![Sincronização completa](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   objetos de saudação agora são atualizados no metaverso hello. Agora, você deseja toolook no objeto Olá Olá metaverso.
2. **Visualização e sincronização completa em um único objeto**  
   Selecione **conectores** na parte superior da saudação. Identificar Olá conector que você fez uma seção anterior do alteração tooin hello, nesse caso Olá serviços de domínio do Active Directory e selecioná-lo. Selecione **Pesquisar Espaço do Conector**. Use um objeto que você deseja alterar de saudação do toouse tootest de toofind de escopo. Selecione o objeto de saudação e clique em **visualização**. Na tela de nova hello, selecione **visualização confirmar**.  
   ![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   alteração de saudação agora é confirmada toohello metaverso.

**Examinar o objeto de saudação no metaverso Olá**  
Agora, você deseja toopick que alguns objetos toomake se Olá valor de exemplo é esperado e regra Olá aplicado. Selecione **pesquisa Metaverse** da parte superior da saudação. Adicione qualquer filtro que você precisa toofind Olá relevantes objetos. Olá resultados de pesquisa, abra um objeto. Examinar os valores de atributo hello e também verificar em Olá **regras de sincronização** coluna Olá regra aplicada conforme o esperado.  
![Pesquisa de metaverso](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Habilitar Olá Agendador
Se tudo estiver como esperado, você pode habilitar o Agendador Olá novamente. No PowerShell, execute `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Outras alterações comuns no fluxo de atributos
seção anterior Olá descritos como toomake tooan o fluxo de atributos é alterado. Nesta seção, são fornecidos alguns exemplos adicionais. etapas de saudação para como a regra de sincronização de saudação toocreate é abreviada, mas você pode encontrar etapas completo Olá na seção anterior hello.

### <a name="use-another-attribute-than-hello-default"></a>Use outro atributo padrão Olá
A Fabrikam, há uma floresta onde o alfabeto local Olá é usado para o nome, sobrenome e nome para exibição. Olá representação de caracteres latinos desses atributos pode ser encontrada em atributos de extensão de saudação. Ao criar a lista de endereços global Olá no Azure AD e Office 365, Olá organização deseja que essas toobe atributos usados em vez disso.

Com uma configuração padrão, um objeto da floresta local Olá tem esta aparência:  
![Fluxo de atributos 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

toocreate uma regra com outros fluxos de atributo, Olá a seguir:

* Iniciar **Editor de regra de sincronização** saudação do menu de início.
* Com **entrada** toohello ainda selecionado, botão esquerdo Olá **adicionar nova regra**.
* Dê a regra de saudação um nome e uma descrição. Selecione tipos de objeto relevantes Olá local do Active Directory e hello. Em **Tipo de Link**, selecione **Junção**. Para a precedência, escolha um número que não seja usado por outra regra. regras de fora da caixa de saudação iniciam com 100, para que o valor de saudação 50 pode ser usado neste exemplo.
  ![Fluxo de atributos 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Deixar o escopo vazio (ou seja, deve aplicar tooall objetos de usuário na floresta de saudação).
* Deixe as regras de associação vazias (que é, permitem Olá qualquer junção de identificador de regra de caixa de saída).
* Nas transformações, crie hello fluxos a seguir:  
  ![Fluxo de atributos 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Clique em **adicionar** toosave regra de saudação.
* Vá muito**Synchronization Service Manager**. Em **conectores**, selecione Olá onde adicionamos a regra de saudação do conector. Selecione **Executar** e **Sincronização Completa**. Uma sincronização completa recalcula todos os objetos usando as regras atuais da saudação.

Este é o resultado Olá Olá mesmo objetos com essa regra personalizada:  
![Fluxo de atributos 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Comprimento de atributos
Atributos de cadeia de caracteres são por padrão conjunto toobe indexáveis e comprimento máximo de saudação é de 448 caracteres. Se você estiver trabalhando com atributos de cadeia de caracteres que podem conter mais, faça a seguir Olá tooinclude-se no fluxo de atributo hello:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Alterando o userPrincipalSuffix Olá
atributo de userPrincipalName Olá no Active Directory nem sempre é conhecido por usuários hello e pode não ser adequado como Olá ID de entrada. Hello Azure AD Connect, o Assistente de instalação de sincronização permite escolher um atributo diferente, por exemplo de email. Mas, em alguns Olá casos atributo deve ser calculado. Por exemplo, empresa Olá Contoso tem dois diretórios do AD do Azure, um para produção e outro para teste. Quiserem usuários Olá em seu teste de locatário toouse outro sufixo da saudação ID de entrada.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

Nesta expressão, take tudo à esquerda da saudação primeiro @-sign (Word) e concatenar com uma cadeia de caracteres fixa.

### <a name="convert-a-multi-value-tooa-single-value"></a>Converter um valor único tooa de múltiplos valores
Alguns atributos no Active Directory são múltiplos no esquema Olá mesmo que pareçam único com o valor em computadores e usuários do Active Directory. Um exemplo é o atributo de descrição de saudação.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

Nesta expressão no caso de atributo Olá tem um valor, levar Olá primeiro item (Item) no atributo hello, remover espaços à direita e (Trim) e, em seguida, mantenha Olá 448 primeiros caracteres (à esquerda) na cadeia de caracteres de saudação.

### <a name="do-not-flow-an-attribute"></a>Não faça um atributo fluir
Para obter informações sobre o cenário de saudação para essa seção, consulte [controlar o processo de fluxo de atributo Olá](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Há duas maneiras toonot fluxo de um atributo. Olá primeiro está disponível no Assistente de instalação hello e permite que você muito[remover atributos selecionados](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Essa opção funciona se você nunca tiver sincronizado atributo Olá antes. No entanto, se você tiver começado toosynchronize esse atributo e posteriormente removê-lo com esse recurso, o mecanismo de sincronização Olá parar de gerenciar o atributo hello e valores existentes de saudação são deixados no AD do Azure.

Se você deseja tooremove Olá valor de um atributo e certifique-se de não fluem em Olá futura, você precisa criar uma regra personalizada.

Na Fabrikam, percebemos que alguns hello, sincronizar toohello de atributos de nuvem não devem ser existe. Queremos toomake-se de que esses atributos são removidos do AD do Azure.  
![Atributos de Extensão Ruins](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Criar uma nova regra de sincronização de entrada e popular a descrição de saudação ![descrições](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Criar fluxos de atributo de tipo **expressão** e com origem Olá **AuthoritativeNull**. Olá literal **AuthoritativeNull** indica que o valor de saudação deve ser vazio em Olá MV mesmo se uma regra de sincronização de precedência inferior tenta toopopulate valor de saudação.
  ![Transformação dos Atributos de Extensão](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Salve Olá regra de sincronização. Iniciar **serviço de sincronização**, localize Olá conector, selecione **executar**, e **sincronização completa**. Esta etapa recalculará todos os fluxos de atributo.
* Verifique se que Olá pretendido alterações são sobre toobe exportado pesquisando o espaço do conector hello.
  ![Exclusão em etapas](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Criar regras com o PowerShell
Usando o editor de regra de sincronização Olá funciona bem quando você tiver apenas alguns toomake de alterações. Se você precisar toomake muitas alterações, o PowerShell pode ser uma opção melhor. Alguns recursos avançados só estão disponíveis com o PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Obter o script do PowerShell Olá para uma regra de caixa de saída
Olá toosee script do PowerShell que criou uma regra de caixa de saída, uma regra de select Olá na sincronização Olá regras editor e clique em **exportar**. Isso proporciona ação Olá PowerShell script regra Olá criado.

### <a name="advanced-precedence"></a>Precedência avançada
regras de sincronização de fora da caixa de saudação começar com um valor de precedência de 100. Se você tiver várias florestas e você precisar toomake muitas alterações personalizadas e as regras de sincronização 99 talvez não seja suficiente.

Você pode instruir Olá mecanismo de sincronização que você deseja regras adicionais inseridas antes das regras de fora da caixa de saudação. tooget esse comportamento, siga estas etapas:

1. Regra de sincronização de fora da caixa primeiro marca hello (essa regra é hello **em de ingresso de usuário do AD**) no editor de regras de sincronização hello e selecione **exportar**. Copie o valor de identificador SR de saudação.  
![PowerShell antes da alteração](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Crie nova regra de sincronização hello. Você pode usar o hello toocreate de editor de regra de sincronização-lo. Exporte o script do PowerShell Olá regra tooa.
3. Na propriedade Olá **PrecedenceBefore**, inserir um valor de identificador de saudação da regra de fora da caixa de saudação. Saudação de conjunto **precedência** muito**0**. Verifique se o atributo de identificador Olá é exclusivo e você não estiver reutilizando um GUID de outra regra. Também verifique se esse Olá **ImmutableTag** propriedade não estiver definida; esta propriedade só deve ser definida para uma regra de caixa de saída. Salve o script do PowerShell hello e executá-lo. resultado de saudação é que a regra personalizada é atribuída o valor de precedência de saudação de 100 e todas as outras regras de caixa de saída são incrementadas.  
![PowerShell após a alteração](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

Você pode ter várias regras de sincronização personalizadas usando Olá mesmo **PrecedenceBefore** valor quando necessário.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Habilitar a sincronização de PreferredDataLocation
Conexão do AD do Azure oferece suporte à sincronização de saudação **PreferredDataLocation** atributo **usuário** objetos na versão 1.1.524.0 e depois. Mais especificamente, as seguintes alterações foram introduzidas:

* esquema de saudação do tipo de objeto Olá **usuário** no hello conector AD do Azure é estendido tooinclude PreferredDataLocation atributo, que é do tipo cadeia de caracteres e é o único valor.

* esquema de saudação do tipo de objeto Olá **pessoa** no hello metaverso é estendido tooinclude PreferredDataLocation atributo, que é do tipo cadeia de caracteres e é o único valor.

Por padrão, o atributo de PreferredDataLocation Olá não está habilitado para sincronização porque não há nenhum atributo PreferredDataLocation correspondente no Active Directory no local. Você deve habilitar a sincronização manualmente.

> [!IMPORTANT]
> Atualmente, Azure AD permite que o atributo de PreferredDataLocation Olá no sincronizado objetos de usuário e nuvem toobe de objetos de usuário configurada diretamente usando o PowerShell do AD do Azure. Depois que você tiver ativado a sincronização do atributo de PreferredDataLocation hello, você deve parar de usar atributo de saudação do PowerShell do Azure AD tooconfigure **sincronizados objetos de usuário** como do Azure AD Connect substituirão-las com base em valores de atributo de origem de saudação no Active Directory no local.

> [!IMPORTANT]
> Em 1 de setembro de 2017, AD do Azure não permitirá mais atributos de PreferredDataLocation Olá em **sincronizados objetos de usuário** toobe configurada diretamente usando o PowerShell do AD do Azure. atributo PreferredLocation tooconfigure sincronizado objetos de usuário, você deve usar o Azure AD Connect somente.

Antes de habilitar a sincronização do atributo de PreferredDataLocation hello, faça o seguinte:

 * Primeiro, decida quais toobe de atributo do Active Directory local usada como atributo de origem de saudação. Ele deve ser do tipo **cadeia de caracteres** e ter **valor único**.

 * Se já tiver configurado o atributo de PreferredDataLocation Olá em existente sincronizado objetos de usuário no AD do Azure usando o PowerShell do AD do Azure, você deve **backport** toohello objetos de usuário correspondentes de valores de atributo de saudação no Active Directory no local.
 
    > [!IMPORTANT]
    > Se você fizer não backport Olá atributo valores toohello correspondentes objetos de usuário no Active Directory no local, do Azure AD Connect removerá os valores de atributo existentes Olá no AD do Azure quando a sincronização para o atributo de PreferredDataLocation Olá estiver habilitado.

 * É recomendável configurar o atributo de origem de saudação em pelo menos dois locais usuário AD objetos agora, que pode ser usado para verificação posterior.
 
sincronização de tooenable etapas saudação do atributo de PreferredDataLocation Olá pode ser resumida como:

1. Desabilitar o agendador de sincronização e verificar se não há nenhuma sincronização em andamento

2. Adicionar toohello de atributo de origem Olá conector AD local esquema

3. Adicionar o esquema do PreferredDataLocation toohello conector AD do Azure

4. Criar um valor de atributo sincronização de entrada regra tooflow saudação do Active Directory no local

5. Criar uma sincronização de saída regra tooflow Olá atributo valor tooAzure AD

6. Executar o ciclo de Sincronização Completa

7. Habilitar o agendador de sincronização

> [!NOTE]
> Olá restante desta seção abrange em detalhes essas etapas. Eles são descritos no contexto de saudação de uma implantação do AD do Azure com a topologia de floresta única e sem regras de sincronização personalizadas. Se você tiver várias floresta topologia, regras de sincronização personalizadas configuradas ou tem um servidor de preparo, necessário etapas de saudação tooadjust adequadamente.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Etapa 1: desabilitar o agendador de sincronização e verificar se não há nenhuma sincronização em andamento
Certifique-se de que nenhuma sincronização ocorre enquanto você estiver no meio de saudação de sincronização de atualização não intencional de tooavoid regras altera sendo exportados tooAzure AD. Agendador de sincronização interna do hello toodisable:

 1. Inicie sessão do PowerShell no servidor do Azure AD Connect hello.

 2. Desabilite a sincronização agendada executando o cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Iniciar Olá **Synchronization Service Manager** pelo vai tooSTART → serviço de sincronização.
 
 4. Vá toohello **operações** guia e confirmar que não há nenhuma operação cujo status seja *"em"andamento.*

![Synchronization Service Manager – verificar se não há nenhuma operação em andamento](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Etapa 2: Adicionar toohello de atributo de origem Olá conector AD local esquema
Nem todos os atributos do AD são importados para Olá espaço do conector AD local. tooadd Olá fonte toohello lista atributos Olá importados atributos:

 1. Vá toohello **conectores** guia Olá Synchronization Service Manager.
 
 2. Clique duas vezes em Olá **conector AD local** e selecione **propriedades**.
 
 3. Na caixa de diálogo pop-up hello, vá toohello **selecionar atributos** guia.
 
 4. Verifique se o atributo de origem de saudação é verificado na lista de atributos de saudação.
 
 5. Clique em **Okey** toosave.

![Adicionar atributo de origem tooon-local esquema conector AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Etapa 3: Adicionar o esquema do PreferredDataLocation toohello conector AD do Azure
Por padrão, o atributo de PreferredDataLocation Olá não é importado para Olá espaço de conectar do Azure AD. tooadd Olá PreferredDataLocation toohello lista de atributos de atributos importados:

 1. Vá toohello **conectores** guia Olá Synchronization Service Manager.

 2. Clique duas vezes em Olá **conector AD do Azure** e selecione **propriedades**.

 3. Na caixa de diálogo pop-up hello, vá toohello **selecionar atributos** guia.

 4. Verifique se o atributo de PreferredDataLocation de saudação é verificado na lista de atributos de saudação.

 5. Clique em **Okey** toosave.

![Adicionar atributo de origem tooAzure esquema de conector AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Etapa 4: Criar um valor de atributo sincronização de entrada regra tooflow saudação do Active Directory no local
regra de sincronização de entrada Hello permite Olá tooflow de valor de atributo do atributo de origem de saudação do local do Active Directory toohello metaverso:

1. Iniciar Olá **Editor de regras de sincronização** pelo vai tooSTART → Editor de regras de sincronização.

2. Filtro de pesquisa de saudação do conjunto **direção** toobe **entrada**.

3. Clique em **adicionar nova regra** botão toocreate uma nova regra de entrada.

4. Em Olá **descrição** guia, forneça Olá a seguinte configuração:
 
    | Atributo | Valor | Detalhes |
    | --- | --- | --- |
    | Nome | *Fornecer um nome* | Por exemplo, *"Entrada do AD – PreferredDataLocation do usuário"* |
    | Descrição | *Fornecer uma descrição* |  |
    | Sistema Conectado | *Escolher local do hello conector AD* |  |
    | Tipo de Objeto do Sistema Conectado | **Usuário** |  |
    | Tipo de Objeto de Metaverso | **Pessoa** |  |
    | Tipo de link | **Join** |  |
    | Precedência | *Escolha um número entre 1 e 99* | 1 a 99 são reservados para regras de sincronização personalizadas. Não selecione um valor que seja usado por outra regra de sincronização. |

5. Vá toohello **filtro de escopo** guia e adicionar um **único grupo de filtro de escopo com hello cláusula a seguir**:
 
    | Atributo | Operador | Valor |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Usuário\_ | 
 
    O filtro de escopo determina a quais objetos AD locais essa regra de sincronização de entrada é aplicada. Neste exemplo, usamos Olá mesmo filtro de escopo usado como *"no AD – usuário Common"* regra de sincronização OOB, que impede que a regra de sincronização Olá seja aplicado tooUser objetos criados por meio de write-back de usuário do AD do Azure recurso. Talvez seja necessário um filtro de escopo de saudação do tootweak de acordo com o tooyour implantação do Azure AD Connect.

6. Vá toohello **guia transformação** e implementar Olá regra de transformação a seguir:
 
    | Tipo de Fluxo | Atributo de Destino | Fonte | Aplicar Uma Vez | Tipo de mesclagem |
    | --- | --- | --- | --- | --- |
    | Direta | PreferredDataLocation | Selecione o atributo de origem Olá | Desmarcado | Atualização |

7. Clique em **adicionar** toocreate regra de entrada hello.

![Criar regra de sincronização de entrada](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Etapa 5: Criar uma sincronização de saída regra tooflow Olá atributo valor tooAzure AD
regra de sincronização de saída de Hello permite Olá tooflow de valor de atributo do atributo do hello metaverso toohello PreferredDataLocation no AD do Azure:

1. Vá toohello **regras de sincronização** Editor.

2. Filtro de pesquisa de saudação do conjunto **direção** toobe **saída**.

3. Clique no botão **Adicionar nova regra**.

4. Em Olá **descrição** guia, forneça Olá a seguinte configuração:

    | Atributo | Valor | Detalhes |
    | --- | --- | --- |
    | Nome | *Fornecer um nome* | Por exemplo, "Out tooAAD – PreferredDataLocation do usuário" |
    | Descrição | *Fornecer uma descrição* |
    | Sistema Conectado | *Selecione o conector do AAD Olá* |
    | Tipo de Objeto do Sistema Conectado | Usuário ||
    | Tipo de Objeto de Metaverso | **Pessoa** ||
    | Tipo de link | **Join** ||
    | Precedência | *Escolha um número entre 1 e 99* | 1 a 99 são reservados para regras de sincronização personalizadas. Não selecione um valor que seja usado por outra regra de sincronização. |

5. Vá toohello **filtro de escopo** guia e adicionar um **único grupo de filtro de escopo com duas cláusulas**:
 
    | Atributo | Operador | Valor |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Usuário |
    | cloudMastered | NOTEQUAL | True  |

    Filtro de escopo determina a quais objetos do Azure AD essa regra de sincronização de saída é aplicada. Neste exemplo, usamos Olá mesmo filtro de escopo de "Limite tooAD – a identidade do usuário" regra de sincronização OOB. Ele impede que regra de sincronização Olá objetos tooUser aplicado que não são sincronizados do Active Directory no local. Talvez seja necessário um filtro de escopo de saudação do tootweak de acordo com o tooyour implantação do Azure AD Connect.
    
6. Vá toohello **transformação** guia e implementar Olá regra de transformação a seguir:

    | Tipo de Fluxo | Atributo de Destino | Fonte | Aplicar Uma Vez | Tipo de mesclagem |
    | --- | --- | --- | --- | --- |
    | Direta | PreferredDataLocation | PreferredDataLocation | Desmarcado | Atualização |

7. Fechar **adicionar** toocreate regra de saída de hello.

![Criar regra de sincronização de saída](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Etapa 6: executar o ciclo de Sincronização Completa
Em geral, o ciclo completo de sincronização é necessário desde que adicionamos Olá de tooboth novos atributos AD e o esquema de conector AD do Azure e introduzidos regras de sincronização personalizadas. É recomendável que você verifique alterações de saudação antes de exportá-los tooAzure AD. Você pode usar as seguintes alterações de saudação do etapas tooverify durante a execução manual de etapas de saudação que formam um ciclo completo de sincronização de saudação. 

1. Executar **importação completa** etapa Olá **conector AD local**:

   1. Vá toohello **operações** guia Olá Synchronization Service Manager.

   2. Clique duas vezes em Olá **conector AD local** e selecione **executar...**

   3. Na caixa de diálogo pop-up hello, selecione **importação completa** e clique em **Okey**.
    
   4. Aguarde a operação toocomplete.

    > [!NOTE]
    > Você pode ignorar a importação completa em Olá AD conector local se o atributo de origem de saudação já está incluído na lista de saudação de atributos importados. Em outras palavras, você não tinha toomake qualquer alteração durante [etapa 2: Adicionar toohello de atributo de origem Olá conector AD local esquema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Executar **importação completa** etapa Olá **conector AD do Azure**:

   1. Clique duas vezes em Olá **conector AD do Azure** e selecione **executar...**

   2. Na caixa de diálogo pop-up hello, selecione **importação completa** e clique em **Okey**.
   
   3. Aguarde a operação toocomplete.

3. Verifique se as alterações de regra de sincronização Olá em um objeto de usuário existente:

atributo de origem de saudação do local do Active Directory e PreferredDataLocation do AD do Azure foram importados para Olá respectivo espaço do conector. Antes de continuar com a etapa de sincronização completa, é recomendável que você faça uma **visualização** em um usuário existente do objeto no hello local espaço do conector AD. objeto Olá selecionado deve ter o atributo de origem de Olá preenchido. Êxito em uma **visualização** com hello PreferredDataLocation preenchido no hello metaverso é um bom indicador que você tenha configurado regras de sincronização Olá corretamente. Para obter informações sobre como toodo uma **visualização**, consulte toosection [verificar se houve alteração Olá](#verify-the-change).

4. Executar **sincronização completa** etapa Olá **conector AD local**:

   1. Clique duas vezes em Olá **conector AD local** e selecione **executar...**
  
   2. Na caixa de diálogo pop-up hello, selecione **sincronização completa** e clique em **Okey**.
   
   3. Aguarde a operação toocomplete.

5. Verifique se **exportações pendentes** tooAzure AD:

   1. Clique duas vezes em Olá **conector AD do Azure** e selecione **espaço do conector de pesquisa**.

   2. No diálogo pop-up do espaço do conector de pesquisa da saudação:

      1. Definir **escopo** muito**exportar pendente**.
      
      2. Marque todas as três caixas de seleção, incluindo **Adicionar, Modificar e Excluir**.
      
      3. Clique em Olá **pesquisa** lista de saudação do botão tooget de objetos com alterações toobe exportado. alterações de saudação tooexamine para um determinado objeto, clique duas vezes no objeto hello.
      
      4. Verifique se as alterações de saudação são esperadas.

6. Executar **exportar** etapa Olá **conector AD do Azure**
      
   1. Saudação de atalho **conector AD do Azure** e selecione **executar...**
   
   2. Olá executar conector pop-caixa de diálogo, selecione **exportar** e clique em **Okey**.
   
   3. Aguarde a exportação tooAzure AD toocomplete.

> [!NOTE]
> Você pode perceber que Olá etapas não incluem a etapa de sincronização completa hello e exportação em Olá conector AD do Azure. etapas de saudação não são necessárias, como valores de atributo Olá estão fluindo do local do Active Directory tooAzure AD apenas.

### <a name="step-7-re-enable-sync-scheduler"></a>Etapa 7: reabilitar o agendador de sincronização
Habilite novamente o Agendador de sincronização interna hello:

1. Inicie uma sessão do PowerShell.

2. Habilite a sincronização agendada novamente executando o cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre o modelo de configuração de saudação em [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Leia mais sobre a linguagem de expressão Olá em [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
