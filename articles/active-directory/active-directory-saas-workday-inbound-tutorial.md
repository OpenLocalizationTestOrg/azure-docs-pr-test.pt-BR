---
title: "Tutorial: configurar Workday para provisionamento automático de usuário com Azure Active Directory e Active Directory local | Microsoft Docs"
description: Saiba como toouse Workday como fonte de dados de identidade para o Active Directory e o Active Directory do Azure.
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Tutorial: configurar Workday para provisionamento automático de usuário com Azure Active Directory e Active Directory local
Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform tooimport pessoas do Workday no Active Directory e o Active Directory do Azure, com write-back opcional de tooWorkday alguns atributos. 



## <a name="overview"></a>Visão geral

Olá [serviço o provisionamento de usuário do Active Directory do Azure](active-directory-saas-app-provisioning.md) integra Olá [API de RH Workday](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) em ordem tooprovision contas de usuário. AD do Azure usa esse Olá tooenable de conexão fluxos de trabalho de provisionamento do usuário a seguir:

* **Provisionamento de usuários tooActive Directory** -sincronizar conjuntos selecionados de usuários do dia útil para uma ou mais florestas do Active Directory. 

* **Provisionamento de usuários somente em nuvem tooAzure do Active Directory** -usuários híbrido que existem no Active Directory e o Active Directory do Azure podem ser provisionados no hello este último usando [AAD Connect](connect/active-directory-aadconnect.md). No entanto, os usuários que são somente em nuvem podem ser provisionados diretamente do dia de trabalho usando o Active Directory tooAzure Olá serviço de provisionamento de usuário do AD do Azure.

* **Write-back de email endereços tooWorkday** -serviço de provisionamento de usuário de saudação do AD do Azure pode gravar selecionado do AD do Azure usuário atributos back tooWorkday, como endereço de email de saudação.

### <a name="scenarios-covered"></a>Cenários cobertos

usuário do Workday Olá provisionamento fluxos de trabalho suportados pelo serviço de provisionamento do usuário de AD do Azure Olá habilita a automação de Olá cenários de gerenciamento de ciclo de vida de recursos humanos e identidade a seguir:

* **Os novos funcionários de contratação** - quando um funcionário novo é adicionado tooWorkday, uma conta de usuário será criada automaticamente no Active Directory, o Active Directory do Azure e, opcionalmente, Office 365 e [outros aplicativos SaaS com suporte pelo AD do Azure ](active-directory-saas-app-provisioning.md), a gravação da saudação tooWorkday de endereço de email.

* **Atualizações de perfil e atributo de funcionário** - Quando um registro de funcionário é atualizado no Workday (como seu nome, cargo ou gerente), sua conta de usuário será atualizada automaticamente no Active Directory, no Azure Active Directory e, opcionalmente, no Office 365 e [outros aplicativos SaaS com suporte do Azure AD](active-directory-saas-app-provisioning.md).

* **Rescisão de funcionário** - Quando um funcionário é rescindido no Workday, sua conta de usuário será desabilitada automaticamente no Active Directory, no Azure Active Directory e, opcionalmente, no Office 365 e [outros aplicativos SaaS com suporte do Azure AD](active-directory-saas-app-provisioning.md).

* **Funcionário novamente contratações** - quando um funcionário é rehired no Workday, sua conta antiga pode ser reativada automaticamente ou Reprovisionado (dependendo de sua preferência) tooActive Directory, Active Directory do Azure e, opcionalmente, o Office 365 e [outros aplicativos SaaS com suporte pelo AD do Azure](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Planejando sua solução

Antes de começar a integração da Workday, verifique os pré-requisitos de saudação abaixo e leia hello seguindo a orientação sobre como toomatch sua arquitetura atual do Active Directory e os requisitos com o provisionamento de usuário Olá soluções fornecidas pelo Azure Active Diretório.

### <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura do Azure AD Premium P1 válida com acesso de administrador global
* Um locatário de implementação do Workday para fins de integração e teste
* Permissões de administrador no Workday toocreate um usuário de integração do sistema e fazer alterações tootest funcionário dados para fins de teste
* Para provisionamento tooActive diretório de usuário, um servidor ingressado no domínio executando o serviço do Windows 2012 ou superior é necessário toohost Olá [agente de sincronização local](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) para a sincronização entre Active Directory e Azure AD

> [!NOTE]
> Se o seu locatário do AD do Azure está localizado na Europa, consulte Olá [problemas conhecidos](#known-issues) seção abaixo.


### <a name="solution-architecture"></a>Arquitetura da solução

AD do Azure fornece um rico conjunto de conectores toohelp que resolver o gerenciamento de ciclo de vida de identidades e provisionamento da Workday tooActive diretório AD do Azure, aplicativos SaaS e além de provisionamento. Quais recursos você usará e como configurar a solução de saudação irão variar dependendo do ambiente e requisitos de sua organização. Como uma primeira etapa, execute o estoque de quantos seguinte Olá estejam presentes e implantado em sua organização:

* Quantas Florestas do Active Directory estão em uso?
* Quantos Domínios do Active Directory estão em uso?
* Quantas OUs (unidades organizacionais) do Active Directory estão em uso?
* Quantos locatários do Azure Active Directory estão em uso?
* Existem usuários que precisam de tooboth toobe provisionado do Active Directory e Azure Active Directory (por exemplo, usuários de "híbrida")?
* Existem usuários que precisam de tooAzure toobe provisionado do Active Directory, mas não no Active Directory (por exemplo, "nuvem somente" usuários)?
* Endereços de email do usuário são necessário toobe gravado tooWorkday?

Uma vez que as respostas toothese perguntas, você pode planejar seu dia de trabalho provisionamento implantação pelo seguinte orientação Olá abaixo.

#### <a name="using-provisioning-connector-apps"></a>Utilizando aplicativos de conectores de provisionamento

O Azure Active Directory dá suporte a conectores de provisionamento pré-integrados para Workday e um grande número de outros aplicativos SaaS. 

Um único conector provisionamento interfaces com hello API do sistema de uma única fonte e ajuda a provisão dados tooa destino único sistema. A maioria dos conectores de provisionamento que dá suporte ao AD do Azure são para uma única origem e o sistema de destino (por exemplo, o AD do Azure tooServiceNow) e podem ser configurado, simplesmente adicionando o aplicativo hello em questão da Galeria de aplicativos do AD do Azure hello (por exemplo, ServiceNow). 

Há uma relação um-para-um entre instâncias de conectores de provisionamento e instâncias de aplicativos no Azure AD:

| Sistema de origem | Sistema de destino |
| ---------- | ---------- | 
| Locatário do Azure AD | Aplicativo SaaS |


No entanto, ao trabalhar com o Workday e o Active Directory, há toobe de sistemas de origem e destino vários considerado:

| Sistema de origem | Sistema de destino | Observações |
| ---------- | ---------- | ---------- |
| Workday | Floresta do Active Directory | Cada floresta é tratada como um sistema de destino distinto |
| Workday | Locatário do Azure AD | Conforme necessário para os usuários somente na nuvem |
| Floresta do Active Directory | Locatário do Azure AD | Atualmente, esse fluxo é tratado pelo AAD Connect |
| Locatário do Azure AD | Workday | Para fazer write-back de endereços de email |

toofacilitate esses vários fluxos de trabalho toomultiple origem e destino sistemas AD do Azure fornece vários aplicativos provisionamento do conector que você pode adicionar da Galeria de aplicativos de saudação do AD do Azure:

![Galeria de Aplicativos do AAD](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **Dia útil tooActive o provisionamento de diretório** -este aplicativo facilita o provisionamento de conta de usuário do Workday tooa floresta do Active Directory. Se você tiver várias florestas, você pode adicionar uma instância deste aplicativo da Galeria de aplicativos do AD do Azure Olá para cada floresta do Active Directory para que é necessário tooprovision.

* **Dia útil tooAzure AD provisionamento** -enquanto a conexão AAD é a ferramenta de saudação que deve ser usado toosynchronize do Active Directory usuários tooAzure do Active Directory, esse aplicativo pode ser usado toofacilitate provisionamento de usuários somente em nuvem do Workday tooa único Locatário do Active Directory do Azure.

* **Write-back WORKDAY** -write-back de endereços de email do usuário do Active Directory do Azure tooWorkday facilita a este aplicativo.

> [!TIP]
> Olá regular "Workday" aplicativo é usado para configurar o logon único entre o dia de trabalho e o Active Directory do Azure. 

Como tooset e configurar esses especial provisionamento de aplicativos do conector é o assunto Olá Olá restantes seções deste tutorial. Quais aplicativos você escolher tooconfigure dependerá de quais sistemas você precisa tooprovision e a quantidade de florestas do Active Directory e do AD do Azure locatários estão em seu ambiente.

![Visão geral](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Configurar um usuário de integração de sistema no Workday
Um requisito comum de todos os conectores de provisionamento do Workday Olá é que eles exigem credenciais para uma instalação do Workday sistema integração conta tooconnect toohello API de RH Workday. Esta seção descreve como a conta toocreate integrador de sistema no dia de trabalho.

> [!NOTE]
> É possível toobypass esse procedimento e em vez disso, use uma conta de administrador global do Workday como conta de integração do sistema de saudação. Isso pode funcionar aparentemente bem para demonstrações, mas não é recomendável para implementações de produção.

### <a name="create-an-integration-system-user"></a>Criar um usuário do sistema de integração

**toocreate um usuário do sistema de integração:**

1. Entre no locatário do Workday utilizando uma conta Administrador. Em Olá **Workday Workbench**, digite criar usuário na caixa de pesquisa hello e, em seguida, clique em **criar usuário do sistema de integração**. 
   
    ![Criar Usuário](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Criar Usuário")
2. Olá completa **criar usuário do sistema de integração** tarefa fornecendo um nome de usuário e senha para um novo usuário do sistema de integração.  
 * Deixe Olá **exigir nova senha no próximo logon** opção desmarcada, porque esse usuário fará logon por meio de programação. 
 * Deixe Olá **minutos de tempo limite de sessão** com seu valor padrão de 0, que impedirá que sessões do usuário de saudação do tempo limite prematuramente. 
   
    ![Criar Usuário do Sistema de Integração](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Criar Usuário do Sistema de Integração")

### <a name="create-a-security-group"></a>Adicionar um grupo de segurança
Você precisa de um grupo de segurança do sistema de integração sem restrição de toocreate e atribuir Olá tooit de usuário.

**toocreate um grupo de segurança:**

1. Insira criar grupo de segurança na caixa de pesquisa hello e, em seguida, clique em **criar grupo de segurança**. 
   
    ![Criar Grupo de Segurança](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "Criar Grupo de Segurança")
2. Olá completa **criar grupo de segurança** tarefa.  
3. Selecionar grupo de segurança de sistema de integração – sem restrição de saudação **tipo do grupo de segurança com locatário** lista suspensa.
4. Crie um toowhich do grupo de segurança membros serão adicionados explicitamente. 
   
    ![Criar Grupo de Segurança](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "Criar Grupo de Segurança")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Atribuir o grupo de segurança toohello do usuário de sistema de integração Olá

**usuário do sistema de integração tooassign hello:**

1. Insira o grupo de segurança de edição na caixa de pesquisa de saudação e, em seguida, clique em **Editar grupo de segurança**. 
   
    ![Editar Grupo de Segurança](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Editar Grupo de Segurança")
2. Procure e selecione o novo grupo de segurança de integração Olá por nome. 
   
    ![Editar Grupo de Segurança](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Editar Grupo de Segurança")
3. Adicione Olá nova integração sistema usuário toohello novo grupo de segurança. 
   
    ![Grupo de Segurança do Sistema](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "Grupo de Segurança do Sistema")  

### <a name="configure-security-group-options"></a>Configurando opções de grupo de segurança
Nesta etapa, você conceda toohello novo grupo permissões de segurança para **obter** e **colocar** operações em objetos Olá protegidos por Olá políticas de segurança de domínio a seguir:

* Provisionamento de conta externa
* Dados de trabalho: Relatórios de trabalho público
* Dados de trabalho: Todas as posições
* Dados de trabalho: Informações atuais sobre a equipe
* Dados de trabalho: Cargo de negócios no perfil de trabalhado

**Opções de grupo de segurança tooconfigure:**

1. Insira as políticas de segurança de domínio na caixa de pesquisa hello e, em seguida, clique no link de saudação **políticas de segurança de domínio para a área funcional**.  
   
    ![Políticas de Segurança de Domínio](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Políticas de Segurança de Domínio")  
2. Pesquisa do sistema e selecione Olá **sistema** área funcional.  Clique em **OK**.  
   
    ![Políticas de Segurança de Domínio](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Políticas de Segurança de Domínio")  
3. Na lista de saudação de políticas de segurança para Olá área funcional sistema, expanda **administração de segurança** e selecione a política de segurança de domínio Olá **provisionamento de conta externa**.  
   
    ![Políticas de Segurança de Domínio](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Políticas de Segurança de Domínio")  
4. Clique em **editar permissões**e, em seguida, em Olá **editar permissões**caixa de diálogo de página, adicione Olá nova segurança grupo toohello lista de grupos de segurança com **obter** e **Colocar** permissões de integração. 
   
    ![Editar Permissão](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Editar Permissão")  
5. Repita a etapa 1 acima tooreturn toohello tela para selecionar as áreas funcionais e desta vez, pesquise "pessoal", selecione Olá **pessoal área funcional** e clique em **Okey**.
   
    ![Políticas de Segurança de Domínio](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Políticas de Segurança de Domínio")  
6. Na lista de saudação de políticas de segurança para Olá área funcional pessoal, expanda **dados do trabalhador: pessoal** e repita a etapa 4 acima para cada uma dessas políticas de segurança restantes:

   * Dados de trabalho: Relatórios de trabalho público
   * Dados de trabalho: Todas as posições
   * Dados de trabalho: Informações atuais sobre a equipe
   * Dados de trabalho: Cargo de negócios no perfil de trabalhado
   
7. Repita a etapa 1, acima, tooreturn toohello tela selecionando áreas funcionais e, desta vez, pesquise **informações de contato**, selecione a área funcional do Olá pessoal e clique em **Okey**.

8.  Na lista de saudação de políticas de segurança para Olá área funcional pessoal, expanda **dados do trabalhador: informações de contato de trabalho**e repita a etapa 4 acima para políticas de segurança Olá abaixo:

    * Dados de trabalho: Email de trabalho

    ![Políticas de Segurança de Domínio](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Políticas de Segurança de Domínio")  
    
### <a name="activate-security-policy-changes"></a>Ativar alterações de política de segurança

**alterações de política de segurança tooactivate:**

1. Insira ativar na caixa de pesquisa hello e, em seguida, clique no link de saudação **ativar alterações de política de segurança pendentes**. 
   
    ![Ativar](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Ativar") 
2. Olá begin ativar alterações de política de segurança pendentes inserindo um comentário para fins de auditoria de tarefas e, em seguida, clique em **Okey**. 
   
    ![Ativar Segurança Pendente](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Ativar Segurança Pendente")   
3. Tarefa concluída Olá na próxima tela hello, marcando a caixa de seleção Olá **confirmar**e, em seguida, clique em **Okey**. 
   
    ![Ativar Segurança Pendente](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Ativar Segurança Pendente")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Configurar provisionamento de usuário do Workday tooActive diretório
Siga a conta de usuário de tooconfigure essas instruções de provisionamento da Workday tooeach floresta do Active Directory que você precisa para o provisionamento.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Adicionar aplicativo de conector provisionamento hello e criar Olá conexão tooWorkday

**tooconfigure Workday tooActive o provisionamento de diretório:**

1.  Vá muito<https://portal.azure.com>

2.  Na barra de navegação à esquerda do hello, selecione **Active Directory do Azure**

3.  Selecione **Aplicativos Empresariais** e, em seguida, **Todos os Aplicativos**.

4.  Selecione **adicionar um aplicativo**e selecione hello **todos os** categoria.

5.  Procurar **tooActive de provisionamento da Workday diretório**e adicionar esse aplicativo da Galeria de saudação.

6.  Após a saudação aplicativo é adicionado e tela de detalhes do aplicativo hello é mostrada, selecione **provisionamento**

7.  Saudação de alteração **provisionamento** **modo** muito**automática**

8.  Olá completa **credenciais de administrador** seção da seguinte maneira:

   * **Admin Username** – insira o nome de usuário de saudação do hello conta do sistema de integração de dia de trabalho, com nome de domínio de locatário Olá acrescentado. **Deve ser semelhante a: username@contoso4**

   * **Senha do administrador –** digite a senha de saudação do hello conta do sistema de integração de dia de trabalho

   * **URL – do locatário** insira Olá URL toohello Workday web services ponto de extremidade para seu locatário. Isso deve parecer com: https://wd3-impl-services1.workday.com/ccx/service/contoso4, onde contoso4 é substituído pelo nome do locatário correto e wd3 impl é substituído pela cadeia de caracteres hello ambiente correto.

   * **Florestas do Active Directory -** hello "Nome" da sua floresta do Active Directory, como retornado pelo Olá Get-ADForest powershell commandlet. Geralmente, é uma cadeia de caracteres como: *contoso.com*

   * **O contêiner do Active Directory -** digite Olá contêiner cadeia de caracteres que contém todos os usuários em sua floresta do AD. Exemplo: *UO= Usuários Padrão,UO=Usuários,DC=contoso,DC=teste*

   * **Email de notificação –** Digite seu endereço de email e marque a caixa de seleção "enviar email se ocorrer falha".

   * Clique em Olá **Conexão de teste** botão. Se o teste de conexão Olá for bem-sucedida, clique em Olá **salvar** botão na parte superior da saudação. Se ele falhar, verifique se credenciais da Workday Olá estão válidas no dia de trabalho. 

![Portal do Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurar mapeamentos de atributos 

Nesta seção, você irá configurar o fluxo de dados de usuário do Workday para o Active Directory.

1.  Na guia de provisionamento de saudação em **mapeamentos**, clique em **tooOnPremises sincronizar trabalhadores da Workday**.

2.  Em Olá **escopo do objeto de origem** campo, você pode selecionar quais conjuntos de usuários no Workday devem estar no escopo para provisionamento tooAD, definindo um conjunto de filtros com base em atributo. escopo do saudação padrão é "todos os usuários no Workday". Filtros de exemplo:

   * Exemplo: Scope toousers com IDs de trabalho entre 1000000 e 2000000

      * Atributo: WorkerID

      * Operador: COINCIDIR.EXREG

      * Valor: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Exemplo: somente funcionários e não trabalhadores contingentes 

      * Atributo: EmployeeID

      * Operador: NÃO NULO

3.  Em Olá **ações do objeto de destino** campo, você pode filtrar globalmente as ações permitidas toobe executada no Active Directory. **Criar** e **Atualizar** são as mais comuns.

4.  Em Olá **mapeamentos de atributo** seção, você pode definir Workday os atributos são mapeados tooActive atributos de diretório.

5. Clique em um tooupdate de mapeamento de atributo existente ou clique **adicionar novo mapeamento** na parte inferior da saudação de novos mapeamentos de saudação tela tooadd. Um mapeamento de atributo individual dá suporte para essas propriedades:

      * **Tipo de mapeamento**

         * **Direto** – grava o valor Olá Olá Workday atributo toohello AD atributo, sem alterações

         * **Constante** -gravar um valor de cadeia de caracteres constante estática para atributo Olá AD

         * **Expressão** – permite que você toowrite um valor personalizado para atributo Olá AD, com base em um ou mais atributos de dia de trabalho. [Para obter mais informações, consulte este artigo sobre expressões](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Atributo de origem** -atributo de usuário de saudação do dia útil.

      * **Valor padrão** – Opcional. Se o atributo de origem Olá tem um valor vazio, o mapeamento de saudação gravará esse valor.
            A configuração mais comum é tooleave em branco.

      * **Atributo de destino** – atributo de saudação do usuário no Active Directory.

      * **Correspondem a objetos que usam esse atributo** – se este mapeamento deve ser usado ou não toouniquely identificar usuários entre dia de trabalho e o Active Directory. Normalmente, isso é definido no campo de ID de trabalho para o dia de trabalho, que normalmente é mapeado para um dos atributos de ID de funcionário Olá no Active Directory.

      * **Precedência de correspondência** – vários atributos de correspondência podem ser definidos. Quando houver múltiplos, os atributos serão avaliados na ordem definida por esse campo. Assim que uma correspondência for encontrada, mais nenhum atributo correspondente será avaliado.

      * **Aplicar esse mapeamento**
       
         * **Sempre** – Aplicar esse mapeamento nas ações de atualização e criação de usuário

         * **Somente durante a criação** - Aplicar esse mapeamento somente nas ações de criação de usuário

6. toosave seus mapeamentos, clique **salvar** na parte superior de saudação da seção de mapeamento de atributo.

![Portal do Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**A seguir, estão alguns exemplos de mapeamentos de atributos entre o Workday e o Active Directory, com algumas expressões comuns**

-   expressão de saudação que mapeia toohello parentDistinguishedName AD atributo pode ser usado tooprovision um tooa de usuário OU específica com base em um ou mais atributos de fonte de dia de trabalho. Este exemplo coloca os usuários em OUs diferentes dependendo dos dados da cidade no Workday.

-   expressão de saudação que mapeia o atributo de userPrincipalName AD toohello criar um UPN de firstName.LastName@contoso.com. Ele também substitui caracteres especiais inválidos.

-   [Há documentação sobre expressões de gravação aqui](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| ATRIBUTO WORKDAY | ATRIBUTO DO ACTIVE DIRECTORY |  ID DE CORRESPONDÊNCIA? | CRIAR / ATUALIZAR |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **Sim** | Gravado na criação somente | 
|  **Município**   |   l   |     | Criar + atualizar |
|  **Empresa**         | company   |     |  Criar + atualizar |
|  **CountryReferenceTwoLetter**      |   co |     |   Criar + atualizar |
| **CountryReferenceTwoLetter**    |  c  |     |         Criar + atualizar |
| **SupervisoryOrganization**  | department  |     |  Criar + atualizar |
|  **PreferredNameData**  |  displayName |     |   Criar + atualizar |
| **EmployeeID**    |  cn    |   |   Gravado na criação somente |
| **Fax**      | facsimileTelephoneNumber     |     |    Criar + atualizar |
| **Nome**   | givenName       |     |    Criar + atualizar |
| **Switch(\[Active\], , "0", "True", "1",)** |  accountDisabled      |     | Criar + atualizar |
| **Móvel**  |    Serviço Móvel       |     |       Gravado na criação somente |
| **EmailAddress**    | mail    |     |     Criar + atualizar |
| **ManagerReference**   | manager  |     |  Criar + atualizar |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Criar + atualizar |
| **PostalCode**  |   postalCode  |     | Criar + atualizar |
| **LocalReference** |  preferredLanguage  |     |  Criar + atualizar |
| **Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**      |    sAMAccountName            |     |         Gravado na criação somente |
| **Sobrenome**   |   sn   |     |  Criar + atualizar |
| **CountryRegionReference** |  st     |     | Criar + atualizar |
| **AddressLineData**    |  streetAddress  |     |   Criar + atualizar |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Gravado na criação somente |
| **BusinessTitle**   |  título     |     |  Criar + atualizar |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**   | userPrincipalName     |     | Criar + atualizar                                                   
| **Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**  | parentDistinguishedName     |     |  Criar + atualizar |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>Parte 3: Configurar o agente de sincronização local Olá

Em ordem tooprovision tooActive diretório local, um agente deve ser instalado em um servidor de domínio em Desejo Olá floresta do Active Directory. Administrador de domínio (ou admin corporativo) as credenciais são necessárias para concluir o procedimento de saudação.

**[Você pode baixar o agente de sincronização de local Olá aqui](https://go.microsoft.com/fwlink/?linkid=847801)**

Depois de instalar o agente, execute comandos do Powershell de saudação abaixo tooconfigure agente de saudação para seu ambiente.

**Comando #1**

> cd C:\\Arquivos de Programa\\Agente de Sincronização do Microsoft Azure Active Directory\\Módulos\\AADSyncAgent

> import-module AADSyncAgent.psd1

**Comando #2**

> Add-ADSyncAgentActiveDirectoryConfiguration

* Entrada: "Como nome do diretório", digite nome da floresta Olá AD, como inserido em parte \#2
* Entrada: nome de usuário e senha de administrador para floresta do Active Directory

**Comando #3**

> Add-ADSyncAgentAzureActiveDirectoryConfiguration

* Entrada: nome de usuário e senha de administrador global para seu locatário do Azure AD

**Comando #4**

> Get-AdSyncAgentProvisioningTasks

* Ação: os dados de confirmação são retornados. Esse comando descobre automaticamente os aplicativos de provisionamento do Workday no seu locatário do Azure AD. Saída de exemplo:

> Nome: Minha Floresta do AD
>
> Habilitado: verdadeiro
>
> DirectoryName : mydomain.contoso.com
>
> Credenciado: falso
>
> Identificador: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Comando #5**

> Start-AdSyncAgentSynchronization -Automatic

**Comando #6**

> net stop aadsyncagent

**Comando #7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>Parte 4: Iniciar serviço de saudação
Depois que concluir partes de 1 a 3, você pode iniciar Olá provisionar um serviço no Portal de gerenciamento de saudação.

1.  Em Olá **provisionamento** guia, Olá conjunto **Status de provisionamento** para **em**.

2. Clique em **Salvar**.

3. Isso iniciará a sincronização inicial hello, que pode levar a um número variável de horas, dependendo de quantos usuários estão no Workday.

4. Eventos de sincronização individuais, como o que os usuários estão sendo lidos fora do dia de trabalho e, em seguida, subsequentemente adicionado ou atualizado tooActive diretório, podem ser exibidos no hello **os Logs de auditoria** guia. **[Consulte Olá provisionamento guia de relatórios para obter instruções detalhadas sobre como os logs de auditoria de saudação tooread](active-directory-saas-provisioning-reporting.md)**

5.  log de aplicativo do Windows Hello no computador do agente Olá mostrará todas as operações executadas por meio do agente de saudação.

6. Após a conclusão, um relatório de resumo de auditoria será gravado na guia **Provisionamento** conforme mostrado abaixo.

![Portal do Azure](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Configurando tooAzure do Active Directory de provisionamento do usuário
Como você configura provisionamento tooAzure do Active Directory dependerá dos requisitos de provisionamento, conforme detalhado na tabela de saudação abaixo.

| Cenário | Solução |
| -------- | -------- |
| **Os usuários precisam toobe provisionado tooActive diretório e o Azure AD** | Utilize o **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Os usuários necessidade toobe provisionado tooActive Directory somente** | Utilize o **[AAD Connect](connect/active-directory-aadconnect.md)** |
| **Os usuários precisam toobe provisionado tooAzure AD apenas (nuvem somente)** | Saudação de uso **Workday tooAzure do Active Directory provisionamento** aplicativo na Galeria de aplicativo hello |

Para obter instruções sobre como configurar a conexão do AD do Azure, consulte Olá [documentação do Azure AD Connect](connect/active-directory-aadconnect.md).

Olá seções a seguir descreve a configuração de uma conexão entre o dia de trabalho e o Azure AD tooprovision somente em nuvem os usuários.

> [!IMPORTANT]
> Apenas siga o procedimento de saudação abaixo se você tiver usuários somente em nuvem que precisam tooAzure toobe provisionado AD e não no Active Directory local.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Adicionar aplicativo de conector provisionamento Olá AD do Azure e criar hello conexão tooWorkday

**tooconfigure Workday tooAzure do Active Directory provisionamento de usuários somente em nuvem:**

1.  Vá muito<https://portal.azure.com>.

2.  Na barra de navegação à esquerda do hello, selecione **Active Directory do Azure**

3.  Selecione **Aplicativos Empresariais** e, em seguida, **Todos os Aplicativos**.

4.  Selecione **adicionar um aplicativo**e, em seguida, selecione Olá **todos os** categoria.

5.  Procurar **Workday tooAzure AD provisionamento**e adicionar esse aplicativo da Galeria de saudação.

6.  Após a saudação aplicativo é adicionado e tela de detalhes do aplicativo hello é mostrada, selecione **provisionamento**

7.  Saudação de alteração **provisionamento** **modo** muito**automática**

8.  Olá completa **credenciais de administrador** seção da seguinte maneira:

   * **Admin Username** – insira o nome de usuário de saudação do hello conta do sistema de integração de dia de trabalho, com nome de domínio de locatário Olá acrescentado. Deve ser semelhante a: username@contoso4

   * **Senha do administrador –** digite a senha de saudação do hello conta do sistema de integração de dia de trabalho

   * **URL – do locatário** insira Olá URL toohello Workday web services ponto de extremidade para seu locatário. Isso deve parecer com: https://wd3-impl-services1.workday.com/ccx/service/contoso4, onde contoso4 é substituído pelo nome do locatário correto e wd3 impl é substituído pela cadeia de caracteres hello ambiente correto (se necessário).

   * **Email de notificação –** Digite seu endereço de email e marque a caixa de seleção "enviar email se ocorrer falha".

   * Clique em Olá **Conexão de teste** botão.

   * Se o teste de conexão Olá for bem-sucedida, clique em Olá **salvar** botão na parte superior da saudação. Se ele falhar, verifique que Olá Workday URL e credenciais são válidas no Workday.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurar mapeamentos de atributos 

Nesta seção, você irá configurar o fluxo dos dados do usuário do Workday para o Azure Active Directory de usuários somente na nuvem.

1.  Na guia de provisionamento de saudação em **mapeamentos**, clique em **tooAzure sincronizar trabalhadores AD**.

2.   Em Olá **escopo do objeto de origem** campo, você pode selecionar quais conjuntos de usuários no Workday devem estar no escopo para provisionamento tooAzure AD, definindo um conjunto de filtros com base em atributo. escopo do saudação padrão é "todos os usuários no Workday". Filtros de exemplo:

   * Exemplo: Scope toousers com IDs de trabalho entre 1000000 e 2000000

      * Atributo: WorkerID

      * Operador: COINCIDIR.EXREG

      * Valor: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Exemplo: Somente trabalhadores contingentes e não funcionários regulares

      * Atributo: ContingentID

      * Operador: NÃO NULO

3.  Em Olá **ações do objeto de destino** campo, você pode filtrar globalmente as ações permitidas toobe executada no AD do Azure. **Criar** e **Atualizar** são as mais comuns.

4.  Em Olá **mapeamentos de atributo** seção, você pode definir Workday os atributos são mapeados tooActive atributos de diretório.

5. Clique em um tooupdate de mapeamento de atributo existente ou clique **adicionar novo mapeamento** na parte inferior da saudação de novos mapeamentos de saudação tela tooadd. Um mapeamento de atributo individual dá suporte para essas propriedades:

   * **Tipo de mapeamento**

      * **Direto** – grava o valor Olá Olá Workday atributo toohello AD atributo, sem alterações

      * **Constante** -gravar um valor de cadeia de caracteres constante estática para atributo Olá AD

      * **Expressão** – permite que você toowrite um valor personalizado para atributo Olá AD, com base em um ou mais atributos de dia de trabalho. [Para obter mais informações, consulte este artigo sobre expressões](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Atributo de origem** -atributo de usuário de saudação do dia útil.

   * **Valor padrão** – Opcional. Se o atributo de origem Olá tem um valor vazio, o mapeamento de saudação gravará esse valor.
            A configuração mais comum é tooleave em branco.

   * **Atributo de destino** – atributo de saudação do usuário no AD do Azure.

   * **Correspondem a objetos que usam esse atributo** – se este mapeamento deve ser usado ou não toouniquely identificar usuários entre dia de trabalho e o Azure AD. Normalmente, isso é definido no campo de ID de trabalho para o dia de trabalho, que normalmente é mapeado para o atributo de ID de funcionário de saudação (novo) ou um atributo de extensão no AD do Azure.

   * **Precedência de correspondência** – vários atributos de correspondência podem ser definidos. Quando houver múltiplos, os atributos serão avaliados na ordem definida por esse campo. Assim que uma correspondência for encontrada, mais nenhum atributo correspondente será avaliado.

   * **Aplicar esse mapeamento**

     * **Sempre** – Aplicar esse mapeamento nas ações de atualização e criação de usuário

     * **Somente durante a criação** - Aplicar esse mapeamento somente nas ações de criação de usuário

6. toosave seus mapeamentos, clique **salvar** na parte superior de saudação da seção de mapeamento de atributo.

### <a name="part-3-start-hello-service"></a>Parte 3: Iniciar serviço de saudação
Depois que concluir partes de 1 a 2, você pode iniciar Olá provisionamento de serviço.

1.  Em Olá **provisionamento** guia, Olá conjunto **Status de provisionamento** para **em**.

2. Clique em **Salvar**.

3. Isso iniciará a sincronização inicial hello, que pode levar a um número variável de horas, dependendo de quantos usuários estão no Workday.

4. Eventos de sincronização individuais podem ser exibidos no hello **os Logs de auditoria** guia. **[Consulte Olá provisionamento guia de relatórios para obter instruções detalhadas sobre como os logs de auditoria de saudação tooread](active-directory-saas-provisioning-reporting.md)**

5. Após a conclusão, um relatório de resumo de auditoria será gravado na guia **Provisionamento** conforme mostrado abaixo.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>Configurar o write-back de tooWorkday de endereços de email
Siga essas tooconfigure do instruções write-back de endereços de email do usuário do Active Directory do Azure tooWorkday.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>Parte 1: Adicionar aplicativo de conector provisionamento hello e criar Olá conexão tooWorkday

**tooconfigure Workday tooActive o provisionamento de diretório:**

1.  Vá muito<https://portal.azure.com>

2.  Na barra de navegação à esquerda do hello, selecione **Active Directory do Azure**

3.  Selecione **Aplicativos Empresariais** e, em seguida, **Todos os Aplicativos**.

4.  Selecione **adicionar um aplicativo**, em seguida, selecione Olá **todos os** categoria.

5.  Procurar **Workday write-back**e adicionar esse aplicativo da Galeria de saudação.

6.  Após a saudação aplicativo é adicionado e tela de detalhes do aplicativo hello é mostrada, selecione **provisionamento**

7.  Saudação de alteração **provisionamento** **modo** muito**automática**

8.  Olá completa **credenciais de administrador** seção da seguinte maneira:

   * **Admin Username** – insira o nome de usuário de saudação do hello conta do sistema de integração de dia de trabalho, com nome de domínio de locatário Olá acrescentado. Deve ser semelhante a: username@contoso4

   * **Senha do administrador –** digite a senha de saudação do hello conta do sistema de integração de dia de trabalho

   * **URL – do locatário** insira Olá URL toohello Workday web services ponto de extremidade para seu locatário. Isso deve parecer com: https://wd3-impl-services1.workday.com/ccx/service/contoso4, onde contoso4 é substituído pelo nome do locatário correto e wd3 impl é substituído pela cadeia de caracteres hello ambiente correto (se necessário).

   * **Email de notificação –** Digite seu endereço de email e marque a caixa de seleção "enviar email se ocorrer falha".

   * Clique em Olá **Conexão de teste** botão. Se o teste de conexão Olá for bem-sucedida, clique em Olá **salvar** botão na parte superior da saudação. Se ele falhar, verifique que Olá Workday URL e credenciais são válidas no Workday.


### <a name="part-2-configure-attribute-mappings"></a>Parte 2: Configurar mapeamentos de atributos 


Nesta seção, você irá configurar o fluxo de dados de usuário do Workday para o Active Directory.

1.  Na guia de provisionamento de saudação em **mapeamentos**, clique em **tooWorkday de usuários do AD do Azure sincronizar**.

2.  Em Olá **escopo do objeto de origem** campo, você pode opcionalmente filtre as quais conjuntos de usuários no Active Directory do Azure devem ter seus endereços de email gravados tooWorkday. escopo do saudação padrão é "todos os usuários no AD do Azure". 

3.  Em Olá **mapeamentos de atributo** seção, você pode definir Workday os atributos são mapeados tooActive atributos de diretório. Há um mapeamento de endereço de email Olá por padrão. No entanto, Olá ID correspondente deve ser atualizada toomatch usuários no AD do Azure com suas entradas correspondentes no Workday. Um método popular de correspondência é ID de trabalho toosynchronize Olá Workday ou funcionário ID tooextensionAttribute1-15 no AD do Azure e, em seguida, use esse atributo em usuários do AD do Azure toomatch no dia de trabalho.

4.  toosave seus mapeamentos, clique **salvar** na parte superior de saudação do hello seção mapeamento de atributo.

### <a name="part-3-start-hello-service"></a>Parte 3: Iniciar serviço de saudação
Depois que concluir partes de 1 a 2, você pode iniciar Olá provisionamento de serviço.

1.  Em Olá **provisionamento** guia, Olá conjunto **Status de provisionamento** para **em**.

2. Clique em **Salvar**.

3. Isso iniciará a sincronização inicial hello, que pode levar a um número variável de horas, dependendo de quantos usuários estão no Workday.

4. Eventos de sincronização individuais podem ser exibidos no hello **os Logs de auditoria** guia. **[Consulte Olá provisionamento guia de relatórios para obter instruções detalhadas sobre como os logs de auditoria de saudação tooread](active-directory-saas-provisioning-reporting.md)**

5. Após a conclusão, um relatório de resumo de auditoria será gravado na guia **Provisionamento** conforme mostrado abaixo.

## <a name="known-issues"></a>Problemas conhecidos

* **Logs em localidades europeus de auditoria** - como versão Olá desta visualização técnica, há um problema conhecido com hello [logs de auditoria](active-directory-saas-provisioning-reporting.md) para aplicativos de conector do Workday Olá não aparecem no hello [doportaldoAzure](https://portal.azure.com) se o locatário de saudação do Azure AD reside em um datacenter europeus. Uma correção para esse problema está próxima. Verifique se esse espaço novamente em Olá próximo futuras atualizações. 

## <a name="additional-resources"></a>Recursos adicionais
* [Tutorial: configurar logon único entre Workday e Azure Active Directory](active-directory-saas-workday-tutorial.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Próximas etapas

* [Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
