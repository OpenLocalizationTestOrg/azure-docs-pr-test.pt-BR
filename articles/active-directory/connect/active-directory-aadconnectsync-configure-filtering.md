---
title: "Configurar a sincronização do Azure AD Connect: configurar a filtragem | Microsoft Docs"
description: "Explica como tooconfigure filtragem na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Sincronização do Azure AD Connect: configurar a filtragem
Com a filtragem, você pode controlar quais objetos do seu diretório local devem aparecer no Azure Active Directory (Azure AD). configuração padrão de saudação usa todos os objetos em todos os domínios em florestas Olá configurado. Em geral, isso é hello configuração recomendada. Os usuários que utilizarem cargas de trabalho do Office 365, como o Exchange Online e o Skype for Business, receberão uma Lista de Endereços Global completa para poderem enviar emails e fazer chamadas para todos. Com a configuração padrão de saudação, eles teriam Olá a que mesma experiência que tiverem com uma implementação de local do Exchange ou o Lync.

Em alguns casos, no entanto, é necessário fazer alguma configuração de padrão de toohello de alterações. Estes são alguns exemplos:

* Planejar Olá toouse [topologia de diretório do AD do multi-Azure](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). Em seguida, você precisa tooapply um toocontrol de filtro que objetos são diretório tooa sincronizado do AD do Azure específico.
* Você executa um piloto para o Azure ou o Office 365 e só deseja um subconjunto de usuários no Azure AD. No piloto pequenos de hello, não é importante toohave uma funcionalidade completa de saudação de toodemonstrate lista de endereços Global.
* Você tem muitas contas de serviço e outras contas não pessoais que não deseja adicionar ao Azure AD.
* Por motivos de conformidade, não exclua contas de usuário locais. Você só pode desabilitá-las. Mas, no AD do Azure, você deseja apenas contas ativas toobe presente.

Este artigo aborda como tooconfigure Olá diferentes métodos de filtragem.

> [!IMPORTANT]
> Microsoft não oferece suporte a modificação ou operação de sincronização do Azure AD Connect fora ações Olá formalmente documentadas. Qualquer uma dessas ações pode resultar em um estado inconsistente ou sem suporte da sincronização do Azure AD Connect. Consequentemente, a Microsoft não pode fornecer suporte técnico para essas implantações.

## <a name="basics-and-important-notes"></a>Noções básicas e observações importantes
No Azure AD Connect Sync, você pode habilitar a filtragem a qualquer momento. Se você iniciar com uma configuração padrão de sincronização de diretório e, em seguida, configurar a filtragem, objetos de saudação que são filtrados não são mais sincronizado tooAzure AD. Devido a essa alteração, quaisquer objetos no Azure AD que foram anteriormente sincronizados, mas filtrados depois, serão excluídos do Azure AD.

Antes de começar a fazer alterações toofiltering, verifique se você [desabilitar a tarefa agendada Olá](#disable-scheduled-task) para que você não exportar acidentalmente as alterações que você ainda não tiver verificado toobe correto.

Porque a filtragem pode remover vários objetos em Olá a mesma hora, você deseja toomake-se de que seus novos filtros estão corretos antes de iniciar a exportação de qualquer tooAzure AD é alterado. Depois de concluir as etapas de configuração Olá, é altamente recomendável que você siga Olá [etapas de verificação](#apply-and-verify-changes) antes de exportar e fazer alterações tooAzure AD.

recurso tooprotect você de excluir muitos objetos por acidente, hello "[impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" é ativado por padrão. Se você excluir muitos objetos devido toofiltering (500 por padrão), você precisa toofollow etapas Olá Olá de tooallow este artigo exclui toogo por meio de tooAzure AD.

Se você usar uma compilação antes de novembro de 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), faça uma alteração da configuração do filtro tooa e usar a sincronização de senha, precisará tootrigger uma sincronização completa de todas as senhas depois de concluir a configuração de saudação. Para obter etapas sobre como tootrigger uma senha de sincronização completa, consulte [disparar uma sincronização completa de todas as senhas](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Se você estiver na compilação 1.0.9125 ou posterior, em seguida, Olá regular **completo sincronização** ação também calcula se as senhas devem ser sincronizadas e se esta etapa adicional não é mais necessária.

Se **usuário** objetos tiverem sido acidentalmente excluídos no AD do Azure devido a um erro de filtragem, você pode recriar objetos de saudação do usuário no AD do Azure removendo as configurações de filtragem. Em seguida, você pode sincronizar os diretórios novamente. Essa ação restaura os usuários de saudação da Lixeira Olá no AD do Azure. Contudo, não é possível cancelar a exclusão de outros tipos de objeto. Por exemplo, se você excluir acidentalmente um grupo de segurança e era usado tooACL um recurso, grupo hello e suas ACLs não podem ser recuperadas.

Azure AD Connect exclui somente os objetos que ele é considerado uma vez toobe no escopo. Se houver objetos no Azure AD criados por outro mecanismo de sincronização e eles não estiverem no escopo, adicionar filtros não os removerá. Por exemplo, se você iniciar com um servidor DirSync que criou uma cópia completa da pasta inteira no AD do Azure e instalar um novo servidor de sincronização do Azure AD Connect em paralelo com filtragem habilitada desde o início do hello, Azure AD Connect não remove Olá extra objetos que são criados pelo DirSync.

configuração de filtragem de saudação é mantida quando você instala ou atualiza tooa a versão mais recente do Azure AD Connect. É sempre uma tooverify de prática recomendada que Olá configuração não foi inadvertidamente alterada após uma versão mais recente atualização tooa antes de executar Olá primeiro ciclo de sincronização.

Se você tiver mais de uma floresta, você deve aplicar o hello filtragem das configurações descritas nesta floresta do tópico tooevery (presumindo que você deseja Olá a mesma configuração para todos eles).

### <a name="disable-hello-scheduled-task"></a>Desabilitar a tarefa agendada Olá
toodisable Olá agendador interno que dispara um ciclo de sincronização a cada 30 minutos, siga estas etapas:

1. Vá tooa PowerShell prompt.
2. Executar `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable Agendador de saudação.
3. Faça alterações de saudação documentados neste artigo.
4. Executar `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable Agendador de saudação novamente.

**Se você usa um build do Azure AD Connect anterior ao 1.1.105.0**  
toodisable Olá tarefa agendada que dispara um ciclo de sincronização a cada três horas, siga estas etapas:

1. Iniciar **Agendador de tarefas** de saudação **iniciar** menu.
2. Diretamente sob **biblioteca do Agendador de tarefas**, localizar Olá tarefa **Azure AD Sync Scheduler**, com o botão direito e selecione **desabilitar**.  
   ![Agendador de Tarefas](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. Você pode fazer alterações de configuração e executar o mecanismo de sincronização de saudação manualmente de saudação **Synchronization Service Manager** console.

Depois de concluir todas as alterações de filtragem, não se esqueça de fazer toocome e **habilitar** novamente a tarefa de saudação.

## <a name="filtering-options"></a>Opções de filtragem
Você pode aplicar Olá, ferramenta de sincronização de diretórios de toohello do configuração tipos filtragem a seguir:

* [**Com base em grupo**](#group-based-filtering): filtragem com base em um único grupo só pode ser configurado na instalação inicial usando o Assistente de instalação de saudação.
* [**Baseado em domínio**](#domain-based-filtering): ao usar essa opção, você pode selecionar quais domínios sincronizar tooAzure AD. Você também pode adicionar e remover domínios de configuração do mecanismo de sincronização hello quando você fizer uma infraestrutura de local de tooyour alterações depois de instalar a sincronização do Azure AD Connect.
* [**Unidade organizacional (UO) – com base em**](#organizational-unitbased-filtering): ao usar essa opção, você pode selecionar quais UOs sincronizar tooAzure AD. Essa opção é para todos os tipos de objeto em UOs selecionadas.
* [**Com base em atributo**](#attribute-based-filtering): ao usar essa opção, você pode filtrar os objetos com base nos valores de atributo em objetos de saudação. Você também pode ter filtros diferentes para tipos de objeto diferentes.

Você pode usar várias opções de filtragem no hello simultaneamente. Por exemplo, você pode usar a filtragem baseada em unidade Organizacional tooonly incluir objetos em uma UO. AT Olá mesmo tempo, você pode usar atributo filtragem toofilter Olá objetos ainda mais. Quando você usa vários métodos de filtragem, os filtros de saudação usam "E" lógico entre os filtros de saudação.

## <a name="domain-based-filtering"></a>Filtragem baseada em domínio
Esta seção fornece Olá etapas tooconfigure o filtro de domínio. Se você adicionou ou removeu domínios na floresta, após a instalação do Azure AD Connect, você também tem Olá tooupdate configuração de filtragem.

Olá preferencial maneira toochange a filtragem baseada em domínio está executando o Assistente de instalação hello e alterando [domínio e a filtragem OU](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Assistente de instalação Olá automatiza todas as tarefas de saudação são documentadas neste tópico.

Siga estes passos apenas se você tiver o Assistente de instalação não é possível toorun Olá por alguma razão.

A configuração de filtragem baseada em domínio consiste nestas etapas:

1. [Selecione os domínios Olá](#select-domains-to-be-synchronized) que você deseja tooinclude na sincronização de saudação.
2. Para cada adicionados e removidos de domínio, ajuste Olá [perfis de execução](#update-run-profiles).
3. [Aplicar e verificar as alterações](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>Selecione Olá domínios toobe sincronizado
domínio de saudação tooset filtrar, Olá seguintes etapas:

1. Entrar no servidor toohello que está executando a sincronização do Azure AD Connect usando uma conta que seja membro da saudação **ADSyncAdmins** grupo de segurança.
2. Iniciar **serviço de sincronização** de saudação **iniciar** menu.
3. Selecione **conectores**e em Olá **conectores** , selecione Olá conector com o tipo de saudação **serviços de domínio do Active Directory**. Em **Ações**, selecione **Propriedades**.  
   ![Propriedades do conector](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Clique em **Configurar Partições de Diretório**.
5. Em Olá **selecionar partições de diretório** lista, selecione e desmarque domínios conforme necessário. Verifique se que somente partições Olá que você deseja toosynchronize sejam selecionadas.  
   ![Partições](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Se você alterado sua infraestrutura do Active Directory local e adicionados ou removidos domínios da floresta hello, clique em Olá **atualização** botão tooget uma lista atualizada. Ao atualizar, você precisará fornecer as credenciais. Forneça as credenciais com acesso de leitura tooWindows servidor Active Directory. Ele não tem um usuário de saudação toobe que é previamente preenchido na caixa de diálogo de saudação.  
   ![Atualização necessária](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Quando tiver terminado, feche Olá **propriedades** caixa de diálogo clicando em **Okey**. Se você tiver removido domínios da floresta Olá, uma mensagem pop-up informando que um domínio foi removido e que a configuração será limpo.
7. Continuar Olá tooadjust [perfis de execução](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Atualizar perfis Olá executar
Se você atualizou o filtro de domínio, também será preciso tooupdate perfis de saudação executar.

1. Em Olá **conectores** lista, certifique-se de que Olá conector que você alterou na etapa anterior hello está selecionado. Em **Ações**, selecione **Configurar Perfis de Execução**.  
   ![Perfis de execução do conector 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Localize e identifique Olá perfis a seguir:
    * Importação completa
    * sincronização total
    * Importação de delta
    * Sincronização de delta
    * Exportação
3. Para cada perfil, ajustar Olá **adicionado** e **removido** domínios.
    1. Para cada um dos perfis de saudação cinco, Olá seguintes etapas para cada **adicionado** domínio:
        1. Selecione o perfil de saudação executar e clique em **nova etapa**.
        2. Em Olá **configurar etapa** página Olá **tipo** menu suspenso, selecione Olá tipo de etapa com hello mesmo nome como saudação de perfil que você está configurando. Em seguida, clique em **Próximo**.  
        ![Perfis de execução do conector 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Em Olá **configuração de conector** página Olá **partição** menu suspenso, o nome de Olá select de domínio Olá que você adicionou tooyour filtro de domínio.  
        ![Perfis de execução do conector 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. Olá tooclose **Configurar perfil de execução** caixa de diálogo, clique em **concluir**.
    2. Para cada um dos perfis de saudação cinco, Olá seguintes etapas para cada **removido** domínio:
        1. Selecione o perfil de saudação executar.
        2. Se hello **valor** de saudação **partição** atributo é um GUID, selecione hello, execute a etapa e clique em **excluir etapa**.  
        ![Perfis de execução do conector 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Verifique se a alteração. Cada domínio que você deseja toosynchronize deve estar listado como uma etapa de cada perfil de execução.
4. Olá tooclose **configurar perfis de execução** caixa de diálogo, clique em **Okey**.
5.  configuração de saudação toocomplete, você precisa toorun um **importação completa** e um **sincronização Delta**. Continuar a ler a seção de saudação [aplicar e verifique se as alterações](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Filtragem baseada em unidade organizacional
Olá preferencial modo toochange a filtragem baseada em unidade Organizacional é executando o Assistente de instalação hello e alterando [domínio e a filtragem OU](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Assistente de instalação Olá automatiza todas as tarefas de saudação são documentadas neste tópico.

Siga estes passos apenas se você tiver o Assistente de instalação não é possível toorun Olá por alguma razão.

tooconfigure organizacional baseada na unidade de filtragem, Olá seguintes etapas:

1. Entrar no servidor toohello que está executando a sincronização do Azure AD Connect usando uma conta que seja membro da saudação **ADSyncAdmins** grupo de segurança.
2. Iniciar **serviço de sincronização** de saudação **iniciar** menu.
3. Selecione **conectores**e em Olá **conectores** , selecione Olá conector com o tipo de saudação **serviços de domínio do Active Directory**. Em **Ações**, selecione **Propriedades**.  
   ![Propriedades do conector](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Clique em **configurar partições de diretório**, selecione domínio Olá que você deseja tooconfigure e, em seguida, clique em **contêineres**.
5. Quando você for solicitado, forneça as credenciais com acesso de leitura tooyour local do Active Directory. Ele não tem um usuário de saudação toobe que é previamente preenchido na caixa de diálogo de saudação.
6. Em Olá **selecionar contêineres** caixa de diálogo, UOs Olá claro que você não deseja toosynchronize diretório na nuvem hello e, em seguida, clique em **Okey**.  
   ![OUs na caixa de diálogo Selecionar contêineres Olá](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Olá **computadores** contêiner deve ser selecionado para sua toobe de computadores Windows 10 sincronizados com êxito tooAzure AD. Se os computadores ingressados no domínio estiverem localizados em outras UOs, verifique se eles estão selecionados.
   * Olá **ForeignSecurityPrincipals** contêiner deve ser selecionado se você tiver várias florestas com relações de confiança. Este contêiner permite toobe de associação de grupo de segurança entre florestas resolvido.
   * Olá **RegisteredDevices** deve ser selecionado OU, se você habilitou o recurso de write-back de dispositivo hello. Se você usar outro recurso de write-back, como o write-back de grupo, verifique se esses locais estão selecionados.
   * Selecione qualquer outra UO, onde usuários, iNetOrgPersons, grupos, contatos e computadores estão localizados. Imagem de hello, todas essas UOs estão localizadas em Olá ManagedObjects OU.
   * Se você usar a filtragem baseada em grupo, Olá OU onde se encontra o grupo de saudação deve ser incluído.
   * Observe que você pode configurar se novas OUs são adicionadas após a conclusão da configuração de filtragem de saudação são sincronizadas ou não sincronizadas. Consulte a próxima seção Olá para obter detalhes.
7. Quando tiver terminado, feche Olá **propriedades** caixa de diálogo clicando em **Okey**.
8. configuração de saudação toocomplete, você precisa toorun um **importação completa** e um **sincronização Delta**. Continuar a ler a seção de saudação [aplicar e verifique se as alterações](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Sincronizar novas UOs
As novas UOs criadas após a configuração da filtragem são sincronizadas por padrão. Esse estado é indicado por uma marca de seleção na caixa. Você também pode cancelar a seleção de alguns subunidades organizacionais. tooget esse comportamento, clique em caixa Olá até ela ficar branca com uma marca de seleção azul (seu estado padrão). Em seguida, desmarque qualquer sub-UOs que você não deseja toosynchronize.

Se todas as sub-UOs estiverem sincronizadas, caixa Olá é branca com uma marca de seleção azul.  
![UO com todas as caixas selecionadas](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Se alguns sub-UOs foram desmarcados, caixa Olá é cinza com uma marca de seleção branca.  
![UO com algumas subunidades organizacionais desmarcadas](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

Com essa configuração, uma nova UO que foi criada em ManagedObjects será sincronizada.

Assistente de instalação do Hello Azure AD Connect sempre cria essa configuração.

### <a name="dont-synchronize-new-ous"></a>Não sincronizar novas UOs
Você pode configurar a sincronização de saudação mecanismo toonot sincronizar novas OUs após a configuração de filtragem de saudação. Esse estado é indicado no hello da interface do usuário pela caixa Olá que aparecem em cinza sólido com nenhuma marca de seleção. tooget esse comportamento, clique em caixa Olá até ela ficar branca com nenhuma marca de seleção. Em seguida, selecione Olá sub-UOs que você deseja toosynchronize.

![OU com raiz Olá desmarcada](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

Com essa configuração, uma nova UO que foi criada em ManagedObjects não será sincronizada.

## <a name="attribute-based-filtering"></a>Filtragem baseada em atributo
Certifique-se de que você está usando Olá novembro de 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) ou uma versão mais recente para essas etapas toowork.

Filtragem baseada em atributo é de objetos de toofilter de forma mais flexíveis hello. Você pode usar a capacidade de saudação do [provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol quase todos os aspectos de quando um objeto é sincronizada tooAzure AD.

Você pode aplicar [entrada](#inbound-filtering) filtragem do Active Directory toohello metaverso, e [saída](#outbound-filtering) filtragem de saudação metaverso tooAzure AD. É recomendável que você aplique a filtragem de entrada porque é toomaintain mais fácil de saudação. Você só deve usar a filtragem de saída se toojoin objetos de mais de uma floresta é necessário antes de avaliação Olá podem ocorrer.

### <a name="inbound-filtering"></a>Filtragem de entrada
Filtragem de entrada usa configuração padrão de hello, onde objetos indo tooAzure AD devem ter Olá atributo de metaverso cloudFiltered não definido tooa valor toobe sincronizado. Se o valor do atributo está definido muito**True**, em seguida, o objeto Olá não está sincronizado. Ele não deve ser definido muito**False**, por design. toomake se outras regras tem Olá capacidade toocontribute um valor, esse atributo só deve valores de saudação toohave **True** ou **nulo** (ausente).

Filtragem de entrada, você usa potência de saudação do **escopo** toodetermine que objetos toosynchronize ou não sincronizados. Isso é onde você fazer ajustes toofit requisitos da sua organização. Olá escopo módulo tem um **grupo** e um **cláusula** toodetermine quando uma regra de sincronização está no escopo. Um grupo contém uma ou muitas cláusulas. Há um “E” lógico entre várias cláusulas e um “OU” lógico entre vários grupos.

Vamos examinar um exemplo:   
![Escopo](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Isso deve ser lido como **(departamento = TI) OU (departamento = Vendas E c = EUA)**.

Em hello a seguir exemplos e etapas, use o objeto de usuário hello como um exemplo, mas você pode usar isso para todos os tipos de objeto.

Em Olá exemplos a seguir, o valor de precedência de saudação começa com 50. Isso pode ser qualquer número não usado, mas deve ser inferior a 100.

#### <a name="negative-filtering-do-not-sync-these"></a>Filtragem negativa, “não sincronizar estes”
Nas Olá exemplo a seguir, você filtrar (não sincronizar) todos os usuários onde **extensionAttribute15** tem valor Olá **NoSync**.

1. Entrar no servidor toohello que está executando a sincronização do Azure AD Connect usando uma conta que seja membro da saudação **ADSyncAdmins** grupo de segurança.
2. Iniciar **Editor de regras de sincronização** de saudação **iniciar** menu.
3. Verifique se a opção **Entrada** está selecionada e clique em **Adicionar Nova Regra**.
4. Dê um nome descritivo, a regra de saudação, como "*no AD – User DoNotSyncFilter*". Floresta correta Olá Select, select **usuário** como Olá **tipo de objeto do CS**e selecione **pessoa** como Olá **tipo de objeto MV**. Em **Tipo de Link**, selecione **Junção**. Em **Precedência**, digite um valor que não esteja sendo usado atualmente por outra regra de sincronização (por exemplo, 50). Em seguida, clique em **Avançar**.  
   ![Descrição da entrada 1](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. Em **Filtro de escopo**, clique em **Adicionar Grupo** e em **Adicionar Cláusula**. Em **Atributo**, selecione **ExtensionAttribute15**. Verifique se **operador** está definido muito**igual**e digite o valor de saudação **NoSync** em Olá **valor** caixa. Clique em **Avançar**.  
   ![Escopo da entrada 2](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Deixe Olá **ingressar** regras vazio e, em seguida, clique em **próximo**.
7. Clique em **adicionar transformação**, selecione Olá **FlowType** como **constante**e selecione **cloudFiltered** como Olá  **Atributo de destino**. Em Olá **fonte** caixa de texto, digite **True**. Clique em **adicionar** toosave regra de saudação.  
   ![Transformação da entrada 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. configuração de saudação toocomplete, você precisa toorun um **sincronização completa**. Continuar a ler a seção de saudação [aplicar e verifique se as alterações](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filtragem positiva: "sincronizar somente estas"
Expressar positivo filtragem pode ser mais difícil porque você também tem tooconsider objetos que não sejam óbvio toobe sincronizado, como salas de conferência. Também é filtro padrão do andamento toooverride Olá na regra de out-of-box Olá **na entrada do AD – ingresso de usuário**. Quando você cria seu filtro personalizado, certifique-se de toonot incluir objetos críticos do sistema, objetos de conflitos de replicação, caixas de correio especiais e as contas de serviço de saudação do Azure AD Connect.

opção de filtragem positivo Olá requer duas regras de sincronização. É necessário uma regra (ou vários) com escopo correto de saudação do toosynchronize de objetos. Você também precisa de uma segunda regra de sincronização pega-tudo que filtra todos os objetos ainda não identificados como um objeto a ser sincronizado.

No hello exemplo a seguir, você sincronizar apenas os objetos de usuário em que o atributo de departamento Olá tem valor de saudação **vendas**.

1. Entrar no servidor toohello que está executando a sincronização do Azure AD Connect usando uma conta que seja membro da saudação **ADSyncAdmins** grupo de segurança.
2. Iniciar **Editor de regras de sincronização** de saudação **iniciar** menu.
3. Verifique se a opção **Entrada** está selecionada e clique em **Adicionar Nova Regra**.
4. Dê um nome descritivo, a regra de saudação, como "*no AD – usuário vendas sincronizar*". Floresta correta Olá Select, select **usuário** como Olá **tipo de objeto do CS**e selecione **pessoa** como Olá **tipo de objeto MV**. Em **Tipo de Link**, selecione **Junção**. Em **Precedência**, digite um valor que não esteja sendo usado atualmente por outra regra de sincronização (por exemplo, 51). Em seguida, clique em **Avançar**.  
   ![Descrição da entrada 4](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. Em **Filtro de escopo**, clique em **Adicionar Grupo** e em **Adicionar Cláusula**. Em **Atributo**, selecione **Departamento**. Certifique-se de que o operador está definido muito**igual**e digite o valor de saudação **vendas** em Olá **valor** caixa. Clique em **Avançar**.  
   ![Escopo da entrada 5](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Deixe Olá **ingressar** regras vazio e, em seguida, clique em **próximo**.
7. Clique em **adicionar transformação**, selecione **constante** como Olá **FlowType**e selecione hello **cloudFiltered** como Olá  **Atributo de destino**. Em Olá **fonte** , digite **False**. Clique em **adicionar** toosave regra de saudação.  
   ![Transformação da entrada 6](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Esse é um caso especial em que você definir explicitamente cloudFiltered muito**False**.
8. Agora temos regra de sincronização pega-tudo toocreate hello. Dê um nome descritivo, a regra de saudação, como "*no AD – filtro de usuário pega-tudo*". Floresta correta Olá Select, select **usuário** como Olá **tipo de objeto do CS**e selecione **pessoa** como Olá **tipo de objeto MV**. Em **Tipo de Link**, selecione **Junção**. Em **Precedência**, digite um valor que não esteja sendo usado atualmente por outra Regra de Sincronização (por exemplo, 99). Você selecionou um valor de precedência que é superior (menor precedência) que a regra de sincronização anterior hello. Mas você também deixou algum espaço para que você pode adicionar mais regras de filtragem de sincronização mais tarde, quando desejar toostart sincronizando departamentos adicionais. Clique em **Avançar**.  
   ![Descrição da entrada 7](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Deixe **Filtro de escopo** vazio e clique em **Avançar**. Um filtro vazio indica regra Olá toobe aplicada tooall objetos.
10. Deixe Olá **ingressar** regras vazio e, em seguida, clique em **próximo**.
11. Clique em **adicionar transformação**, selecione **constante** como Olá **FlowType**e selecione **cloudFiltered** como Olá  **Atributo de destino**. Em Olá **fonte** , digite **True**. Clique em **adicionar** toosave regra de saudação.  
    ![Transformação da entrada 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. configuração de saudação toocomplete, você precisa toorun um **sincronização completa**. Continuar a ler a seção de saudação [aplicar e verifique se as alterações](#apply-and-verify-changes).

Se você precisar, você pode criar mais regras do tipo primeiro hello, onde você incluir mais objetos na sincronização de saudação.

### <a name="outbound-filtering"></a>Filtragem de saída
Em alguns casos, é necessário toodo Olá filtragem somente depois Olá objetos tiverem ingressado no metaverso hello. Por exemplo, ele pode ser necessário toolook no atributo de mensagem de saudação da floresta de recursos hello e atributo do hello userPrincipalName da floresta de conta hello, toodetermine se um objeto deve ser sincronizado. Nesses casos, você deve criar hello filtragem na regra de saída de hello.

Neste exemplo, você alterar Olá filtragem para que somente os usuários que têm os emails e userPrincipalName que terminam em @contoso.com são sincronizados:

1. Entrar no servidor toohello que está executando a sincronização do Azure AD Connect usando uma conta que seja membro da saudação **ADSyncAdmins** grupo de segurança.
2. Iniciar **Editor de regras de sincronização** de saudação **iniciar** menu.
3. Em **Tipos de Regra**, clique em **Saída**.
4. Regra de saudação localizar denominada **Out tooAAD – ingresso de usuário**e clique em **editar**.
5. No pop-up hello, responder **Sim** toocreate uma cópia da regra de saudação.
6. Em Olá **descrição** página, altere **precedência** tooan valor não utilizado, como 50.
7. Clique em **filtro de escopo** Olá navegação esquerda e, em seguida, clique em **Adicionar cláusula**. Em **Atributo**, selecione **mail**. Em **Operador**, selecione **ENDSWITH**. Em **Valor**, digite **@contoso.com** e clique em **Adicionar cláusula**. Em **Atributo**, selecione **userPrincipalName**. Em **Operador**, selecione **ENDSWITH**. Em **Valor**, digite **@contoso.com**.
8. Clique em **Salvar**.
9. configuração de saudação toocomplete, você precisa toorun um **sincronização completa**. Continuar a ler a seção de saudação [aplicar e verifique se as alterações](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Aplicar e verificar as alterações
Depois que você fez as alterações de configuração, você deve aplicá-las toohello objetos que já estão presentes no sistema de saudação. Também pode ser que os objetos de saudação que não estão atualmente no mecanismo de sincronização de saudação devem ser processados (e mecanismo de sincronização de saudação precisa que o sistema de origem de saudação tooread tooverify novamente seu conteúdo).

Se você alterou a configuração de saudação usando **domínio** ou **unidade organizacional** filtragem, em seguida, você precisa toodo um **importação completa**, seguido por **Delta sincronização**.

Se você alterou a configuração de saudação usando **atributo** filtragem, em seguida, você precisa toodo um **completo sincronização**.

Olá seguintes etapas:

1. Iniciar **serviço de sincronização** de saudação **iniciar** menu.
2. Selecione **Conectores**. Em Olá **conectores** , selecione Olá conector onde você fez uma alteração de configuração anterior. Em **Ações**, selecione **Executar**.  
   ![Execução do conector](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. Em **perfis de execução**, selecione Olá operação que foi mencionada na seção anterior hello. Se você precisar toorun duas ações, execução Olá segundo após Olá primeiro for concluída. (Olá **estado** coluna é **ocioso** para conector de saudação selecionada.)

Após a sincronização de hello, todas as alterações são preparado toobe exportado. Antes de realmente fazer alterações de saudação no AD do Azure, você deseja tooverify que todas essas alterações estão corretas.

1. Inicie um prompt de comando e vá muito`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Execute `csexport "Name of Connector" %temp%\export.xml /f:x`.  
   nome de saudação do hello conector é no serviço de sincronização. Ele tem um too"contoso.com de nome semelhante – AAD" do AD do Azure.
3. Execute `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`.
4. Agora você tem um arquivo em %temp% chamado export.csv que pode ser examinado no Microsoft Excel. Esse arquivo contém todas as alterações de saudação significam toobe exportado.
5. Faça as alterações necessárias Olá toohello dados ou configuração e execute estas etapas novamente (importar, sincronizar e verifique se) até Olá alterações sobre toobe exportado são que o esperado.

Quando estiver satisfeito, exporte Olá alterações tooAzure AD.

1. Selecione **Conectores**. Em Olá **conectores** , selecione Olá conector AD do Azure. Em **Ações**, selecione **Executar**.
2. Em **Perfis de execução**, selecione **Exportar**.
3. Se as alterações de configuração excluem muitos objetos, você ver um erro na exportação de saudação quando o número de saudação é maior que o limite configurada de saudação (por padrão, 500). Se você vir esse erro, você precisará tootemporarily desabilitar hello "[impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" recurso.

Agora é Agendador de saudação do tempo tooenable novamente.

1. Iniciar **Agendador de tarefas** de saudação **iniciar** menu.
2. Diretamente sob **biblioteca do Agendador de tarefas**, localizar Olá tarefa **Azure AD Sync Scheduler**, com o botão direito e selecione **habilitar**.

## <a name="group-based-filtering"></a>Filtragem baseada em grupo
Você pode configurar Olá filtragem baseada em grupo a primeira vez que você instale o Azure AD Connect usando [instalação personalizada](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). Ele destina-se uma implantação piloto onde você deseja que apenas um pequeno conjunto de objetos toobe sincronizado. Se você desabilitar a filtragem baseada em grupo, ela não poderá ser habilitada novamente. Ele tem *não tem suporte* toouse filtragem em uma configuração personalizada com base em grupo. Ele tem somente tem suporte tooconfigure esse recurso usando o Assistente de instalação de saudação. Quando tiver concluído o piloto, em seguida, usar uma saudação outras opções de filtragem neste tópico. Ao usar a filtragem com base na UO em conjunto com a filtragem baseada em grupo, Olá OU(s) encontram grupo hello e seus membros deve ser incluído.

Durante a sincronização de várias florestas do AD, você pode configurar a filtragem baseada em grupo com a especificação de um grupo diferente para cada conector do AD. Se desejar toosynchronize um usuário em uma floresta do AD e hello mesmo usuário tem um ou mais correspondente FSP (entidade de segurança externa) objetos em outras florestas do AD, deve garantir que esse objeto de usuário hello e todos os seus correspondente objetos FSP estão dentro baseado em grupo escopo de filtragem. Se um ou mais dos objetos FSP Olá são excluídos por filtragem baseada em grupo, o objeto de usuário Olá não será sincronizado tooAzure AD.

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre a configuração da [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md).
- Saiba mais sobre a [integração de identidades locais com o Azure AD](active-directory-aadconnect.md).
