---
title: "espaços de trabalho aaaManage no portal do OMS Azure Log Analytics e hello | Microsoft Docs"
description: "Você pode gerenciar espaços de trabalho no portal do OMS Azure Log Analytics e hello usando uma variedade de tarefas administrativas em usuários, contas, espaços de trabalho e contas do Azure."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Gerenciar espaços de trabalho

toomanage acesso tooLog análise, você executar várias tarefas administrativas e relacionadas tooworkspaces. Este artigo fornece procedimentos e recomendações sobre espaços de trabalho de toomanage de prática recomendada. Um espaço de trabalho é essencialmente um contêiner que inclui informações de conta e informações de configuração simples para a conta de saudação. Você ou outros membros de sua organização podem usar vários espaços de trabalho toomanage diferentes conjuntos de dados que são coletados de toda ou de partes da sua infraestrutura de TI.

toocreate um espaço de trabalho, você precisa:

1. Tenho uma assinatura do Azure.
2. Escolher um nome para o espaço de trabalho.
3. Associe o espaço de trabalho de saudação à sua assinatura.
4. Escolher uma localização geográfica.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Determinar Olá número de espaços de trabalho que você precisa
Um espaço de trabalho é um recurso do Azure e um contêiner em que dados são coletados, agregados, analisados e apresentados em Olá portal do Azure.

Você pode ter vários espaços de trabalho por assinatura do Azure e você pode ter acesso toomore que um espaço de trabalho. Número de saudação minimização de espaços de trabalho permite tooquery e correlaciona através de saudação maioria dos dados, pois ele não é possível tooquery em vários espaços de trabalho. Esta seção descreve quando ele pode ser útil toocreate mais de um espaço de trabalho.

Hoje, um espaço de trabalho fornece:

* Uma localização geográfica para o armazenamento dos dados
* Granularidade de cobrança
* Isolamento dos dados
* Escopo de configuração

Com base em Olá anterior características, convém toocreate vários espaços de trabalho se:

* Você é uma empresa global e precisa de dados armazenados em regiões específicas por motivos de soberania de dados ou conformidade.
* Você estiver usando o Azure e desejar que a transferência de dados de saída tooavoid encargos por ter um espaço de trabalho em Olá mesma região como Olá recursos do Azure, ele gerencia.
* Você deseja tooallocate departamentos de toodifferent de cobranças ou com base no uso de grupos de negócios. Quando você cria um espaço de trabalho para cada departamento ou grupo comercial, a instrução de fatura e uso do Azure mostra encargos Olá para cada espaço de trabalho separadamente.
* Você é um provedor de serviço gerenciado e precisa de dados de análise de log tookeep Olá para cada cliente que você gerencia isolado de outros dados de cliente.
* Gerenciar vários clientes e quiser que cada cliente / departamento / negócios grupo toosee seus próprios dados, mas não os dados de saudação para outras pessoas.

Ao usar agentes toocollect dados, você pode [configurar tooone de tooreport cada agente ou mais espaços de trabalho](log-analytics-windows-agents.md).

Se você estiver usando o System Center Operations Manager, cada grupo de gerenciamento do Operations Manager poderá ser conectado a apenas um espaço de trabalho. Você pode instalar Olá Microsoft Monitoring Agent em computadores gerenciados pelo Operations Manager e ter tooboth de relatório Olá agente do Operations Manager e um espaço de trabalho de análise de Log diferente.

### <a name="workspace-information"></a>Informações do espaço de trabalho

Você pode exibir detalhes sobre o espaço de trabalho Olá portal do Azure. Você também pode exibir detalhes no portal do OMS hello.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Exibir informações de espaço de trabalho no hello portal do Azure

1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com) usando sua assinatura do Azure.
2. Em Olá **Hub** menu, clique em **mais serviços** e, na lista de saudação de recursos, digite **análise de Log**. Como começar a digitar, Olá filtros de lista com base em sua entrada. Clique em **Log Analytics**.  
    ![Hub do Azure](./media/log-analytics-manage-access/hub.png)  
3. Na folha de assinaturas de análise de Log hello, selecione um espaço de trabalho.
4. folha de espaço de trabalho Olá exibe detalhes sobre o espaço de trabalho hello e links para informações adicionais.  
    ![detalhes do espaço de trabalho](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Gerenciar contas e usuários
Cada espaço de trabalho pode ter várias contas associadas a ele, e cada conta (conta da Microsoft ou conta organizacional) pode ter espaços de trabalho do access toomultiple.

Por padrão, conta da Microsoft hello ou conta organizacional que cria o espaço de trabalho de saudação se torna Olá administrador do espaço de trabalho de saudação.

Há dois modelos de permissão que controlam o espaço de trabalho de análise de Log de tooa acesso:

1. Funções de usuário herdadas do Log Analytics
2. [Acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md)

Olá a tabela a seguir resume o acesso de saudação que pode ser definido com o uso de cada modelo de permissão:

|                          | Portal do Log Analytics | Portal do Azure | API (incluindo PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Funções de usuário do Log Analytics | Sim                  | Não           | Não                         |
| Acesso baseado em função do Azure  | Sim                  | Sim          | Sim                        |

> [!NOTE]
> Análise de log é mover toouse acesso baseado em função do Azure como modelo de permissões hello, substituindo as funções de usuário de análise de Log hello.
>
>

Olá herdadas funções de usuário de análise de Log somente controlam acesso tooactivities executadas em Olá [portal da análise de Log](https://mms.microsoft.com).

Olá atividades a seguir também requerem permissões do Azure:

| Ação                                                          | Permissões do Azure necessárias | Observações |
|-----------------------------------------------------------------|--------------------------|-------|
| Adicionar e remover soluções de gerenciamento                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Saudação de alteração de preço                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Exibindo dados em Olá *Backup* e *recuperação de Site* blocos de solução | Administrador/coadministrador | Recursos de acessos implantado usando o modelo de implantação clássico Olá |
| Criar um espaço de trabalho no hello portal do Azure                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Gerenciando acesso tooLog análise usando permissões do Azure
toogrant acesso toohello análise de Log espaço de trabalho usando permissões do Azure, siga as etapas de saudação em [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md).

O Azure tem duas funções de usuário predefinidas para o Log Analytics:
- Leitor do Log Analytics
- Colaborador do Log Analytics

Membros da saudação *leitor de Log de análise de* função pode:
- Exibir e pesquisar todos os dados de monitoramento 
- Exiba configurações de monitoramento, incluindo a exibição de configuração de saudação do diagnóstico do Azure em todos os recursos do Azure.

| Tipo    | Permissão | Descrição |
| ------- | ---------- | ----------- |
| Ação | `*/read`   | Capacidade tooview todos os recursos e a configuração de recurso. Inclui exibir: <br> Status de extensão da máquina virtual <br> Configuração do diagnóstico do Azure nos recursos <br> Todas as propriedades e configurações de todos os recursos |
| Ação | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Consultas de tooperform v2 de pesquisa de Log de capacidade |
| Ação | `Microsoft.OperationalInsights/workspaces/search/action` | Consultas de tooperform v1 de pesquisa de Log de capacidade |
| Ação | `Microsoft.Support/*` | Casos de suporte de tooopen de capacidade |
|Nenhuma Ação | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Impede a leitura do espaço de trabalho chave toouse necessário Olá dados API e tooinstall agentes de coleção |


Membros da saudação *Colaborador de análise de Log* função pode:
- Ler todos os dados de monitoramento 
- Criar e configurar Contas de automação
- Adicionar e remover soluções de gerenciamento
- Ler as chaves da conta de armazenamento 
- Configurar a coleta de logs no Armazenamento do Azure
- Editar configurações de monitoramento dos recursos do Azure, incluindo
  - Adicionando Olá tooVMs de extensão VM
  - Configurar o diagnóstico do Azure em todos os recursos do Azure

> [!NOTE] 
> Você pode usar o hello capacidade tooadd um máquina virtual extensão tooa máquina virtual toogain controle total sobre uma máquina virtual.

| Permissão | Descrição |
| ---------- | ----------- |
| `*/read`     | Capacidade tooview todos os recursos e a configuração de recurso. Inclui exibir: <br> Status de extensão da máquina virtual <br> Configuração do diagnóstico do Azure nos recursos <br> Todas as propriedades e configurações de todos os recursos |
| `Microsoft.Automation/automationAccounts/*` | Capacidade toocreate e configurar contas de automação do Azure, incluindo adicionar e editar runbooks |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Adicionar, atualizar e remover extensões de máquina virtual, incluindo extensão do Microsoft Monitoring Agent hello e hello agente do OMS para Linux extensão |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Chave de conta de armazenamento de saudação de exibição. Necessário tooconfigure logs de tooread de análise de logs de contas de armazenamento do Azure |
| `Microsoft.Insights/alertRules/*` | Adicionar, atualizar e remover as regras de alerta |
| `Microsoft.Insights/diagnosticSettings/*` | Adicionar, atualizar e remover as configurações de diagnóstico nos recursos do Azure |
| `Microsoft.OperationalInsights/*` | Adicionar, atualizar e remover a configuração dos espaços de trabalho do Log Analytics |
| `Microsoft.OperationsManagement/*` | Adicionar e remover soluções de gerenciamento |
| `Microsoft.Resources/deployments/*` | Crie e exclua implantações. Necessário para adicionar e remover soluções, espaços de trabalho e contas de automação |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Crie e exclua implantações. Necessário para adicionar e remover soluções, espaços de trabalho e contas de automação |

tooadd e remover usuários tooa função de usuário, é necessário toohave `Microsoft.Authorization/*/Delete` e `Microsoft.Authorization/*/Write` permissão.

Use essas funções o acesso aos usuários toogive em escopos diferentes:
- Assinatura – espaços de trabalho do Access tooall na assinatura Olá
- Grupo de recursos - espaço de trabalho do Access tooall no grupo de recursos de saudação
- O recurso - Olá de tooonly de acesso especificado espaço de trabalho

Use [funções personalizadas](../active-directory/role-based-access-control-custom-roles.md) toocreate funções com as permissões específicas de saudação necessárias.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Funções de usuário do Azure e funções de usuário do portal do Log Analytics
Se você tiver no Azure pelo menos permissão de leitura no espaço de trabalho de análise de Log hello, você pode abrir o portal da análise de Log Olá clicando Olá **Portal do OMS** ao exibir o espaço de trabalho de análise de Log de saudação de tarefas.

Ao abrir o portal de análise de Log Olá, você pode alternar funções de usuário de análise de Log herdadas do toousing hello. Se você não tiver uma atribuição de função no portal de análise de Log hello, Olá serviço [verificações hello Azure permissões que você tem no espaço de trabalho Olá](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
Sua atribuição de função no portal de análise de Log de saudação é determinada da seguinte maneira:

| Condições                                                   | Funções de usuário do Log Analytics atribuída | Observações |
|--------------------------------------------------------------|----------------------------------|-------|
| Sua conta pertencer a função de usuário de análise de Log herdada tooa     | Olá especificado a função de usuário de análise de Log | |
| Sua conta não pertence a função de usuário de análise de Log herdada tooa <br> Espaço de trabalho de toohello de permissões completo do Azure (`*` permissão <sup>1</sup>) | Administrador ||
| Sua conta não pertence a função de usuário de análise de Log herdada tooa <br> Espaço de trabalho de toohello de permissões completo do Azure (`*` permissão <sup>1</sup>) <br> *sem ações* de `Microsoft.Authorization/*/Delete` e `Microsoft.Authorization/*/Write` | Colaborador ||
| Sua conta não pertence a função de usuário de análise de Log herdada tooa <br> Permissão de leitura do Azure | Somente leitura ||
| Sua conta não pertence a função de usuário de análise de Log herdada tooa <br> Permissões do Azure não são compreendidas | Somente leitura ||
| Para assinaturas de gerenciadas por CSP (Provedor de solução de nuvem) <br> conta Olá com que você está conectado está no espaço de trabalho do hello Azure Active Directory vinculado toohello | Administrador | Normalmente Prezado cliente de um CSP |
| Para assinaturas de gerenciadas por CSP (Provedor de solução de nuvem) <br> conta Olá com que você está conectado não está no espaço de trabalho do hello Azure Active Directory vinculado toohello | Colaborador | Olá normalmente CSP |

<sup>1</sup> consulte muito[permissões do Azure](../active-directory/role-based-access-control-custom-roles.md) para obter mais informações sobre definições de função. Ao avaliar funções, uma ação de `*` não é equivalente muito`Microsoft.OperationalInsights/workspaces/*`.

Tookeep alguns pontos em mente sobre Olá portal do Azure:

* Quando você entrar no portal do OMS toohello usando http://mms.microsoft.com, você verá Olá **selecione um espaço de trabalho** lista. Essa lista só contém espaços de trabalho onde você tem uma função de usuário do Log Analytics. espaços de trabalho do hello toosee você tem acesso toowith Azure assinaturas, você precisa toospecify um locatário como parte da URL de saudação. Por exemplo: `mms.microsoft.com/?tenant=contoso.com`. Identificador do locatário Olá costuma essa última parte Olá endereço de email que você usar toosign no.
* Se você quiser toonavigate diretamente toousing Azure acessar o portal tooa que você tem permissões, você precisa de recursos de saudação do toospecify como parte da URL de saudação. Ele é possível tooget essa URL usando o PowerShell.

  Por exemplo: `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  Olá URL é semelhante a:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Gerenciamento de usuários no portal do OMS Olá
Gerenciar usuários e grupos em Olá **gerenciar usuários** guia em Olá **contas** guia, na página de configurações de saudação.   

![gerenciar usuários](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Adicionar um espaço de trabalho usuário tooan existente
Use Olá etapas tooadd um espaço de trabalho tooa usuário ou grupo a seguir.

1. No portal do OMS hello, clique em Olá **configurações** lado a lado.
2. Clique em Olá **contas** guia e, em seguida, clique em Olá **gerenciar usuários** guia.
3. Em Olá **gerenciar usuários** , escolha Olá tooadd de tipo de conta: **conta organizacional**, **Microsoft Account**, **Microsoft Support**.

   * Se você escolher Account da Microsoft, digite o endereço de email de saudação do usuário Olá associado Olá Account da Microsoft.
   * Se você escolher conta organizacional, digite parte do usuário Olá / alias de email ou o nome do grupo e uma lista de usuários e grupos de correspondência é exibido em uma caixa suspensa. Selecione um usuário ou um grupo.
   * Use Microsoft Support toogive engenheiro Microsoft Support ou outros toohelp de espaço de trabalho do Microsoft funcionário acesso temporário tooyour na solução de problemas.

     > [!NOTE]
     > Para melhor desempenho de hello, limitar o número de saudação de grupos do Active Directory associados a um único toothree de conta do OMS — um para administradores, uma para colaboradores e outro para os usuários somente leitura. Usar mais grupos pode afetar o desempenho de saudação da análise de Log.
     >
     >
4. Escolha o tipo de saudação do usuário ou grupo tooadd: **administrador**, **Colaborador**, ou **usuário ReadOnly**.  
5. Clique em **Adicionar**.

   Se você estiver adicionando uma conta da Microsoft, um espaço de trabalho de saudação do convite toojoin é enviado email toohello fornecido. Depois que o usuário Olá segue instruções Olá Olá convite toojoin OMS, usuário Olá pode acessar o espaço de trabalho de saudação.
   Se você estiver adicionando uma conta organizacional, usuário Olá pode acessar a análise de Log imediatamente.  

#### <a name="edit-an-existing-user-type"></a>Editar um tipo de usuário existente
Você pode alterar a função da conta de saudação de um usuário associado à sua conta do OMS. Você tem Olá função as opções a seguir:

* *Administrador*: pode gerenciar os usuários, exibir e agir em todos os alertas, adicionar e remover servidores
* *Contribuidor*: pode exibir e agir em todos os alertas, adicionar e remover servidores
* *Usuário Somente Leitura*: os usuários marcados como somente leitura não podem:

  1. Adicione/remova as soluções. Galeria de soluções Hello está oculto.
  2. Adicione/modifique/remova os blocos em **Meu Painel**.
  3. Saudação de exibição **configurações** páginas. páginas de saudação estão ocultos.
  4. No modo de exibição de pesquisa de saudação, configuração do Power BI, pesquisas salvas e alertas tarefas estão ocultos.

#### <a name="tooedit-an-account"></a>tooedit uma conta
1. No portal do OMS hello, clique em Olá **configurações** lado a lado.
2. Clique em Olá **contas** guia e, em seguida, clique em Olá **gerenciar usuários** guia.
3. Selecione a função hello usuário Olá que você deseja toochange.
4. Na caixa de diálogo de confirmação de saudação, clique em **Sim**.

### <a name="remove-a-user-from-a-workspace"></a>Remover um usuário de um espaço de trabalho
Use Olá seguir etapas tooremove um usuário de um espaço de trabalho. Remover usuário de saudação não fecha o espaço de trabalho de saudação. Em vez disso, remove Olá associação entre usuário e o espaço de trabalho de saudação. Se um usuário estiver associado a vários espaços de trabalho, esse usuário ainda pode entrar tooOMS e consulte os outros espaços de trabalho.

1. No portal do OMS hello, clique em Olá **configurações** lado a lado.
2. Clique em Olá **contas** guia e, em seguida, clique em Olá **gerenciar usuários** guia.
3. Clique em **remover** próximo nome de usuário toohello que você deseja tooremove.
4. Na caixa de diálogo de confirmação de saudação, clique em **Sim**.

### <a name="add-a-group-tooan-existing-workspace"></a>Adicionar um espaço de trabalho grupo tooan existente
1. Em Olá anterior a seção "tooadd um espaço de trabalho usuário tooan existente", siga as etapas 1 a 4.
2. Em **Escolher Usuário/Grupo**, selecione **Grupo**.  
   ![Adicionar um espaço de trabalho grupo tooan existente](./media/log-analytics-manage-access/add-group.png)
3. Insira o endereço de Email ou nome de exibição de saudação para grupo de saudação você gostaria que tooadd.
4. Selecione o grupo de saudação nos resultados de lista hello e, em seguida, clique em **adicionar**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Vincular um tooan de espaço de trabalho existente a assinatura do Azure
Todos os espaços de trabalho criados depois de 26 de setembro de 2016 devem ser vinculado tooan assinatura do Azure no momento da criação. Espaços de trabalho criados antes dessa data devem ser vinculado tooa espaço de trabalho quando você entrar. Quando você cria o espaço de trabalho de saudação de saudação portal do Azure, ou quando você vincular seu espaço de trabalho tooan assinatura do Azure, Active Directory do Azure está vinculado com sua conta organizacional.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink tooan um espaço de trabalho a assinatura do Azure no portal do OMS Olá

- Quando você entrar no portal do OMS hello, será solicitada tooselect uma assinatura do Azure. Selecione Olá assinatura que você deseja que o espaço de trabalho do toolink tooyour e, em seguida, clique em **Link**.  
    ![Vincular assinatura do Azure](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink um espaço de trabalho, sua conta do Azure já deve ter acesso toohello espaço de trabalho que deseja toolink.  Em outras palavras, conta de saudação usada tooaccess Olá portal do Azure deve ser **Olá mesmo** como conta de Olá, use o espaço de trabalho do tooaccess Olá. Se não, consulte [adicionar um espaço de trabalho usuário tooan existente](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink um assinatura do Azure no portal do Azure de saudação do tooan de espaço de trabalho
1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Procure pelo **Log Analytics** e selecione-o.
3. Você vê sua lista de espaços de trabalho existentes. Clique em **Adicionar**.  
   ![lista de espaços de trabalho](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. No **Espaço de Trabalho do OMS**, clique em **ou no link existente**.  
   ![link existente](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Clique em **Definir configurações obrigatórias**.  
   ![configure required settings](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Consulte a lista de saudação de espaços de trabalho que não são vinculados ainda tooyour conta do Azure. Selecione um espaço de trabalho.  
   ![selecionar espaços de trabalho](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Se necessário, você pode alterar os valores para Olá itens a seguir:
   * Assinatura
   * Grupo de recursos
   * Local padrão
   * Tipo de preço   
     ![alterar valores](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Clique em **OK**. espaço de trabalho Olá agora está vinculado tooyour conta do Azure.

> [!NOTE]
> Se você não vir o espaço de trabalho de saudação você gostaria que toolink, sua assinatura do Azure não tem acesso toohello espaço de trabalho que você criou usando o portal do OMS hello.  conta de toothis toogrant acesso do portal do OMS hello, consulte [adicionar um espaço de trabalho usuário tooan existente](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Atualizar um tooa de espaço de trabalho paga plano
Há três tipos de plano de espaço de trabalho para OMS: **Gratuito**, **Autônomo** e **OMS**.  Se você estiver usando Olá *livre* planejar, há um limite de 500 MB de dados por dia enviadas tooLog análise.  Se você exceder esse valor, será necessário toochange seu espaço de trabalho tooa paga plano tooavoid que não está coletando dados além desse limite. Você pode alterar seu tipo de plano a qualquer momento.  Para obter mais informações sobre os preços do OMS, consulte [Detalhes do Preço](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Usar os direitos de uma assinatura do OMS
direitos de saudação toouse que vêm da aquisição do OMS E1, o OMS E2 OMS ou o complemento do OMS para o System Center, escolha Olá *OMS* plano de análise de logs do OMS.

Quando você comprar uma assinatura do OMS, direitos de saudação são adicionados tooyour Enterprise Agreement. Nenhuma assinatura do Azure que é criada sob este contrato pode usar direitos hello. Todos os espaços de trabalho essas assinaturas usam autorizações do OMS hello.

tooensure uso de um espaço de trabalho é aplicado tooyour direitos de saudação assinatura do OMS, você precisa:

1. Criar seu espaço de trabalho em uma assinatura do Azure que faz parte da saudação Enterprise Agreement que inclui a assinatura do OMS Olá
2. Selecione Olá *OMS* plano para o espaço de trabalho de saudação

> [!NOTE]
> Se o seu espaço de trabalho foi criado antes de 26 de setembro de 2016 e seu plano de preços de análise de Log é *Premium*, em seguida, esse espaço de trabalho usa direitos do complemento do OMS de saudação do System Center. Você também pode usar seus direitos alterando toohello *OMS* preço.
>
>

direitos de assinatura de OMS Olá não são visíveis no hello Azure ou no portal do OMS. Você pode ver os direitos de uso e no hello Portal Empresarial.  

Se você precisar Olá toochange assinatura do Azure que seu espaço de trabalho está vinculado, você pode usar o hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Usar o Azure Commitment de um Enterprise Agreement
Se você não tiver uma assinatura do OMS, você paga separadamente para cada componente do OMS e uso de saudação aparece em sua fatura do Azure.

Se você tiver o Azure investimento em Olá enterprise registro toowhich suas assinaturas do Azure estão vinculadas, uso de análise de Log será automaticamente débito contra Olá restantes confirmação monetária.

Se você precisar toochange hello assinatura do Azure que Olá espaço de trabalho está vinculada, você pode usar o hello Azure PowerShell [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Alterar um tooa de espaço de trabalho paga o preço em Olá portal do Azure
1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Procure pelo **Log Analytics** e selecione-o.
3. Você vê sua lista de espaços de trabalho existentes. Selecione um espaço de trabalho.  
4. Na folha de espaço de trabalho hello, em **geral**, clique em **preço**.  
5. Em **Tipo de preço**, clique em selecionar um tipo de preço e clique em **Selecionar**.  
    ![selecionar plano](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Quando você atualiza o modo de exibição no hello portal do Azure, você verá **preço** atualizado para a camada de saudação selecionado.  
    ![plano atualizado](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Se o seu espaço de trabalho é vinculado tooan conta de automação, antes você pode selecionar Olá *autônomo (por GB)* preço você deve excluir qualquer **automação e controle** soluções e desvincular Olá automação conta. Na folha de espaço de trabalho hello, em **geral**, clique em **soluções** soluções toosee e delete. Olá toounlink conta de automação, clique o nome de saudação do hello conta de automação em Olá **preço** folha.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Alterar um tooa de espaço de trabalho paga o preço no portal do OMS Olá

toochange Olá preço usando o portal do OMS hello, você deve ter uma assinatura do Azure.

1. No portal do OMS hello, clique em Olá **configurações** lado a lado.
2. Clique em Olá **contas** guia e, em seguida, clique em Olá **assinatura do Azure e plano de dados** guia.
3. Clique em Olá deseja toouse de preço.
4. Clique em **Salvar**.  
   ![planos de assinatura e dados](./media/log-analytics-manage-access/subscription-tab.png)

O novo plano de dados é exibido na Olá OMS portal da faixa de opções na parte superior de saudação da sua página da web.

![faixa de opções do OMS](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Alterar o tempo que o Log Analytics leva para armazenar dados

Em Olá livre de preço, análise de Log faz Olá disponível últimos sete dias de dados.
Na faixa de preços padrão Olá, análise de Log torna disponível Olá últimos 30 dias de dados.
Na camada de preços de Premium Olá, análise de Log torna disponível Olá últimos 365 dias de dados.
Olá autônomo e o OMS preços camadas, por padrão, a análise de Log faz Olá disponível últimos 31 dias de dados.

Quando você usa Olá autônomo e camadas de preços do OMS, você pode manter too2 anos de dados (730 dias). Dados armazenados além do padrão de saudação de 31 dias incorre em um encargo de retenção de dados. Para obter mais informações sobre preços, consulte [encargos excedentes](https://azure.microsoft.com/pricing/details/log-analytics/).

comprimento da saudação toochange de retenção de dados:

1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Procure pelo **Log Analytics** e selecione-o.
3. Você vê sua lista de espaços de trabalho existentes. Selecione um espaço de trabalho.  
4. Na folha de espaço de trabalho de saudação em **geral**, clique em **retenção**.  
5. Usar Olá controle deslizante tooincrease ou diminuir Olá número de dias de retenção e, em seguida, clique em **salvar**.  
    ![alterar retenção](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Alterar uma Organização do Azure Active Directory para um espaço de trabalho

Você pode alterar a organização do Azure Active Directory de um espaço de trabalho. Olá alteração organização do Active Directory do Azure permite que você tooadd usuários e grupos no espaço de trabalho toohello directory.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>Olá toochange organização do Active Directory do Azure para um espaço de trabalho

1. Na página de configurações de saudação no portal do OMS hello, clique em **contas** e, em seguida, clique em Olá **gerenciar usuários** guia.  
2. Examinar as informações de saudação sobre contas organizacionais e, em seguida, clique em **alteração organização**.  
    ![alterar organização](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Insira informações de identidade Olá administrador saudação do seu domínio do Active Directory do Azure. Posteriormente, você verá uma confirmação informando que seu espaço de trabalho é o domínio do Active Directory do Azure tooyour vinculado.  
    ![confirmação de espaço de trabalho vinculado](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Excluir um espaço de trabalho do Log Analytics
Quando você excluir um espaço de trabalho de análise de Log, todos os dados relacionados a tooyour de espaço de trabalho é excluído da saudação serviço OMS dentro de 30 dias.

Se você for um administrador e houver vários usuários associados ao espaço de trabalho hello, associação de saudação entre os usuários e o espaço de trabalho Olá será interrompida. Se os usuários de saudação estiverem associados a outros espaços de trabalho, eles podem continuar usando o OMS com esses outros espaços. No entanto, se eles não estiverem associados a outros espaços de trabalho que precisam toocreate toouse um espaço de trabalho do OMS.

### <a name="toodelete-a-workspace"></a>toodelete um espaço de trabalho
1. O logon no hello [portal do Azure](http://portal.azure.com).
2. Procure pelo **Log Analytics** e selecione-o.
3. Você vê sua lista de espaços de trabalho existentes. Selecione o espaço de trabalho de saudação que você deseja toodelete.
4. Na folha de espaço de trabalho de saudação, clique em **excluir**.  
    ![delete](./media/log-analytics-manage-access/delete-workspace01.png)
5. No diálogo de confirmação do hello excluir espaço de trabalho, clique em **Sim**.

## <a name="next-steps"></a>Próximas etapas
* Consulte [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md) tooadd agentes e coletar dados.
* [Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.
* [Definir configurações de proxy e firewall na análise de Log](log-analytics-proxy-firewall.md) se sua organização usa um servidor proxy ou firewall para que os agentes podem se comunicar com hello serviço de análise de Log.
