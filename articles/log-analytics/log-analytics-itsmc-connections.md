---
title: "conexões de aaaITSM no conector de gerenciamento de serviço do OMS TI | Microsoft Docs"
description: "Conecte seus produtos/serviços ITSM com conector de gerenciamento de serviço de TI no OMS toocentrally monitor e gerenciar itens de trabalho ITSM hello."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Conectar produtos/serviços ITSM ao Conector de Gerenciamento do Serviço de TI (Versão Prévia)
Este artigo fornece informações sobre como tooconnect seu produto ou serviço ITSM tooIT conector de gerenciamento de serviço do OMS e centralmente gerenciar seus itens de trabalho. Para saber mais sobre o Conector de Gerenciamento do Serviço de TI, consulte [Visão geral](log-analytics-itsmc-overview.md).

Olá produtos/serviços a seguir têm suporte:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Conectar o System Center Service Manager tooIT conector de gerenciamento de serviço do OMS

Olá, seções a seguir fornecem detalhes sobre como tooconnect o toohello de produto do System Center Service Manager conector de gerenciamento de serviço de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que ter Olá pré-requisitos atendidos a seguir:

- Conector de Gerenciamento do Serviço de TI instalado.
Mais informações: [Configuração](log-analytics-itsmc-overview.md#configuration).
- saudação de aplicativo Web do Service Manager (aplicativo Web) for implantada e configurada. Veja informações sobre o aplicativo Web [aqui](#create-and-deploy-service-manager-web-app-service).
- Conexão híbrida criada e configurada. Obter mais informações: [híbrida de saudação Configurar Conexão](#configure-the-hybrid-connection).
- Versões do Service Manager com suporte: 2012 R2 ou 2016.
- Função de usuário: [Operador avançado](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedimento de conexão

Use Olá seguindo o procedimento tooconnect sua instância de System Center Service Manager toohello conector de gerenciamento de serviço de TI:

1. Vá muito**OMS** >**configurações** > **fontes conectadas**.
2. Selecione **Conector ITSM,**  clique em **Adicionar Nova Conexão**.

    ![Service manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Fornecer informações de saudação conforme descrito em Olá a tabela a seguir e clique em **salvar** toocreate conexão de saudação:

> [!NOTE]
> Todos esses parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Digite um nome para a instância do System Center Service Manager Olá que você deseja tooconnect com hello conector de gerenciamento de serviço de TI.  Use esse nome posteriormente quando você configurar os itens de trabalho nesta instância / exibir a análise de log detalhado. |
| **Selecionar Tipo de conexão**   | Selecione **System Center Service Manager**. |
| **URL do Servidor**   | Digite a URL de saudação do hello aplicativo Web do Service Manager. Veja mais sobre o aplicativo Web do Service Manager [aqui](#create-and-deploy-service-manager-web-app-service).
| **ID do Cliente**   | ID do cliente Olá gerado (usando o script automático Olá) para autenticar o aplicativo Web de saudação do tipo. Para obter mais informações sobre o script hello automatizada são [aqui.](log-analytics-itsmc-service-manager-script.md)|
| **Segredo do Cliente**   | Segredo do cliente do tipo hello, gerada para essa ID.   |
| **Escopo de Sincronização de Dados**   | Selecione itens de trabalho do Service Manager Olá que você deseja toosync por meio de saudação conector de gerenciamento de serviço de TI.  Esses itens de trabalho são importados para o Log Analytics. **Opções:** Incidentes, Solicitações de Alteração.|
| **Sincronizar Dados** | Digite hello número de dias anteriores a que você deseja que os dados de saudação do. **Limite máximo** 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se desejar que os itens de configuração de saudação toocreate produto ITSM da saudação. Quando selecionado, o OMS cria CIs Olá afetado como itens de configuração (no caso de CIs inexistente) Olá suportados sistema ITSM. **Padrão**: desabilitado. |

Quando conectado e sincronizado com êxito:

- Itens de trabalho selecionados do Service Manager são importados para OMS **Log Analytics.** Você pode exibir o resumo de saudação desses itens de trabalho no bloco do conector de gerenciamento de serviço de TI hello.

- Do OMS, você pode criar incidentes de alertas do OMS ou de pesquisa de log nesta instância do Service Manager.

Mais informações: [Criar itens de trabalho ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [Criar itens de trabalho ITSM de logs do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Criar e implantar o serviço de aplicativo Web do Service Manager

tooconnect Olá local Service Manager com hello conector de gerenciamento do serviço de TI no OMS, a Microsoft criou um aplicativo Web do Service Manager no hello GitHub.

tooset backup Olá ITSM Web app para o Gerenciador de serviço, Olá a seguir:

- **Aplicativo de Web Deploy Olá** – implantar o aplicativo da Web de saudação, defina as propriedades de saudação e autenticar com o AD do Azure. Você pode implantar o aplicativo da web de saudação usando Olá [automatizada script](log-analytics-itsmc-service-manager-script.md) que a Microsoft forneceu a você.
- **Configurar conexão do hello híbrida** - [configurar essa conexão](#configure-the-hybrid-connection), manualmente.

#### <a name="deploy-hello-web-app"></a>Implantar o aplicativo da web de saudação
Olá Use automatizada [script](log-analytics-itsmc-service-manager-script.md) toodeploy Olá aplicativo Web, defina propriedades de saudação e autenticar com o AD do Azure.

Execute script hello fornecendo Olá detalhes necessários a seguir:

- Detalhes da assinatura do Azure
- Nome do grupo de recursos
- Local
- Detalhes do servidor do Service Manager (nome do servidor, domínio, nome de usuário e senha)
- Prefixo de nome do site para seu aplicativo Web
- Namespace do ServiceBus.

script Hello cria Olá Web app usando nome hello especificado (junto com alguns toomake de cadeias de caracteres adicionais-exclusivo). Ele gera Olá **URL do aplicativo Web**, **ID do cliente** e **segredo do cliente**.

Salvar valores hello, você usá-los quando você criar uma conexão com o conector de gerenciamento de serviço de TI.

**Verifique a instalação do aplicativo Web Olá**

1. Vá muito**portal do Azure** > **recursos**.
2. Selecione o aplicativo Web de saudação, clique em **configurações** > **configurações de aplicativo**.
3. Confirme informações Olá sobre instância do Gerenciador de serviço Olá fornecidas no tempo de saudação de implantar o aplicativo hello por meio de script hello.

### <a name="configure-hello-hybrid-connection"></a>Configurar conexão do hello híbrido

Use Olá após a conexão híbrida de saudação de tooconfigure de procedimento que se conecta a instância do Service Manager Olá com hello conector de gerenciamento de serviço de TI no OMS.

1. Localize Olá aplicativo Web do Service Manager, em **recursos do Azure**.
2. Clique em **Configurações** > **Rede**.
3. Em **conexões híbridas**, clique em **configurar seus pontos de extremidade de conexão híbrida**.

    ![Rede de conexão híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. Em Olá **conexões híbridas** folha, clique em **Adicionar conexão híbrida**.

    ![Adição de conexão híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. Em Olá **adicionar as conexões híbridas** folha, clique em **híbrida de criar nova Conexão**.

    ![Nova Conexão híbrida](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Digite hello valores a seguir:

    - **Nome do ponto de extremidade**: Especifique um nome para a nova conexão de híbrida hello.
    -  **Host do ponto de extremidade**: FQDN do servidor de gerenciamento do Service Manager hello.
    - **Porta do Ponto de Extremidade**: digite 5724
    - **Namespace ServiceBus**: usar um namespace de barramento de serviço existente ou crie um novo.
    - **Local**: selecione Olá local.
    -  **Nome**: especificar um barramento de serviço do nome toohello se você está criando.

    ![Valores da conexão híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Clique em **Okey** tooclose Olá **criar conexão híbrida** folha e começar a criar a conexão do hello híbrida.

    Depois de criar a conexão do hello híbrida, ele será exibido na folha de saudação.

7. Após a conexão do hello híbrida é criada, selecione a conexão hello e clique em **adicionar selecionada conexão híbrida**.

    ![Nova conexão híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Configure o ouvinte Olá

Saudação de uso após a instalação do procedimento tooconfigure Olá ouvinte para conexão do hello híbrida.

1. Em Olá **conexões híbridas** folha, clique em **Download Olá Gerenciador de Conexão** e instalá-lo no computador Olá onde a instância do System Center Service Manager está em execução.

    Depois de saudação instalação for concluída, **Gerenciador de Conexão híbrida UI** opção está disponível em **iniciar** menu.

2. Clique em **Gerenciador de Conexão híbrida UI** , você será solicitado para suas credenciais do Azure.

3. Faça logon com suas credenciais do Azure e selecione sua assinatura onde Olá conexão híbrida foi criado.

4. Clique em **Salvar**.

Sua conexão híbrida foi conectada com êxito.

![conexão híbrida com êxito](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Após a conexão do hello híbrida é criada, verifique e teste Olá conexão visitando Olá implantado o aplicativo Web do Service Manager. Verifique a conexão Olá foi bem-sucedida antes de tentar tooconnect toohello conector de gerenciamento de serviço de TI no OMS.

Olá imagem a seguir mostra os detalhes de saudação de uma conexão bem-sucedida:

![Teste de conexão híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Conectar o ServiceNow tooIT conector de gerenciamento de serviço do OMS

Olá, seções a seguir fornecem detalhes sobre como tooconnect seu produto de ServiceNow toohello conector de gerenciamento de serviço de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que ter Olá pré-requisitos atendidos a seguir:

- Conector de Gerenciamento do Serviço de TI instalado. Mais informações: [Configuração.](log-analytics-itsmc-overview.md#configuration)
- Versões com suporte do ServiceNow – Fuji, Geneva, Helsinki.

Faça ServiceNow Admins Olá seguinte em sua instância do ServiceNow:
- Gere a ID do cliente e o segredo do cliente para o produto de ServiceNow hello. Para obter informações sobre como toogenerate ID do cliente e o segredo, consulte [configuração OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Instale Olá aplicativo de usuário para integração com o Microsoft OMS (ServiceNow aplicativo). [Saiba mais](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Crie função de usuário de integração para o aplicativo de usuário Olá instalado. Obter informações sobre como é a função de usuário de integração de saudação toocreate [aqui](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procedimento de conexão**

Use Olá procedimento toocreate uma conexão do ServiceNow a seguir:

1. Vá muito**OMS** > **configurações** > **fontes conectadas**.
2. Selecione **Conector ITSM,**  clique em **Adicionar Nova Conexão**.

    ![Conexão do ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Fornecer informações de saudação conforme descrito em Olá a tabela a seguir e clique em **salvar** toocreate conexão de saudação:

> [!NOTE]
> Todos esses parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Digite um nome para a instância do ServiceNow Olá que você deseja tooconnect com hello conector de gerenciamento de serviço de TI.  Use esse nome posteriormente no OMS quando você configurar os itens de trabalho nesse ITSM/exibir o Log Analytics detalhado. |
| **Selecionar Tipo de conexão**   | Selecione **ServiceNow**. |
| **Nome de Usuário**   | Digite o nome de usuário de integração de saudação que você criou na conexão Olá ServiceNow aplicativo toosupport Olá toohello conector de gerenciamento de serviço de TI. Mais informações: [Criar função de usuário de aplicativo do ServiceNow](#create-integration-user-role-in-servicenow-app).|
| **Senha**   | Digite a senha Olá associada com este nome de usuário. **Observação**: nome de usuário e senha são usadas para gerar tokens de autenticação somente e não são armazenadas em qualquer lugar no serviço do OMS hello.  |
| **URL do Servidor**   | Digite a URL de saudação de instância do ServiceNow Olá que você deseja tooconnect tooIT conector do serviço de gerenciamento. |
| **ID do Cliente**   | Digite hello ID do cliente que você deseja toouse para autenticação de OAuth2, que você gerou anteriormente.  Para saber mais sobre como gerar o ID do cliente e o segredo: [configuração OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Segredo do Cliente**   | Segredo do cliente do tipo hello, gerada para essa ID.   |
| **Escopo de Sincronização de Dados**   | Selecione itens de trabalho do ServiceNow Olá que você deseja tooOMS toosync, por meio de saudação conector de gerenciamento de serviço de TI.  valores de saudação selecionado são importados para a análise de log.   **Opções:** Incidentes e Solicitações de Alteração.|
| **Sincronizar Dados** | Digite hello número de dias anteriores a que você deseja que os dados de saudação do. **Limite máximo** 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se desejar que os itens de configuração de saudação toocreate produto ITSM da saudação. Quando selecionado, o OMS cria CIs Olá afetado como itens de configuração (no caso de CIs inexistente) Olá suportados sistema ITSM. **Padrão**: desabilitado. |


Quando conectado e sincronizado com êxito:

- Selecionar trabalho itens de conexão do ServiceNow são importados para o Log Analytics do OMS.  Você pode exibir o resumo de saudação desses itens de trabalho no bloco do conector de gerenciamento de serviço de TI hello.
- Você pode criar incidentes, alertas e eventos de pesquisa de log ou alertas de OMS nesta instância do ServiceNow.  


Mais informações: [Criar itens de trabalho ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [Criar itens de trabalho ITSM de logs do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Criar função de usuário de integração no aplicativo do ServiceNow

Saudação de usuário procedimento a seguir:

1.  Visite Olá [ServiceNow repositório](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) e instalar Olá **aplicativo de usuário para ServiceNow e integração de OMS do Microsoft** em sua instância do ServiceNow.
2.  Após a instalação, visite Olá esquerda da barra de navegação da instância do ServiceNow hello, pesquisa e selecione integrador de OMS do Microsoft.  
3.  Clique em **Lista de Verificação de Instalação**.

    Olá status será exibido como **não concluir** se Olá função de usuário é ainda toobe criado.

4.  No texto de saudação das caixas, em seguida muito**criar usuário de integração**, insira nome de usuário de saudação do usuário Olá que pode se conectar toohello conector de gerenciamento de serviço de TI no OMS.
5.  Insira a senha de saudação para esse usuário e clique em **Okey**.  

>[!NOTE]

> Você pode usar conexão de ServiceNow essas credenciais toomake Olá no OMS.

Olá usuário recém-criado é exibido com funções de padrão de saudação atribuídas.

Funções padrão:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   itil
-   template_editor
-   view_changer

Depois que o usuário Olá é criado com êxito, Olá status de **Verificar lista de verificação de instalação** move tooCompleted, listando os detalhes de Olá Olá da função de usuário criado para o aplicativo hello.

> [!NOTE]

> tooallow toocreate um usuário **alertas** e **eventos** no ServiceNow do OMS:

> - Certifique-se de que ter o módulo de gerenciamento de eventos de saudação instalado na instância do ServiceNow.

> - Adicione Olá usuário de integração de toohello funções a seguir:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Conecte-se Provance tooIT conector de gerenciamento de serviço do OMS

Olá, seções a seguir fornecem detalhes sobre como tooconnect seu produto de Provance toohello conector de gerenciamento de serviço de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que ter Olá pré-requisitos atendidos a seguir:

- Conector de Gerenciamento do Serviço de TI instalado. Mais informações: [Configuração](log-analytics-itsmc-overview.md#configuration).
- Provance aplicativo deve ser registrado com o Azure AD - ID do cliente é disponibilizada. Para obter informações detalhadas, consulte [como a autenticação do active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Função de usuário: Administrador.

### <a name="connection-procedure"></a>Procedimento de Conexão

Use Olá procedimento toocreate uma conexão Provance a seguir:

1. Vá muito**OMS** > **configurações** > **fontes conectadas**.
2. Selecione **Conector ITSM,**  clique em **Adicionar Nova Conexão**.  

    ![Conexão do Provance](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Fornecer informações de saudação conforme descrito em Olá a tabela a seguir e clique em **salvar** toocreate conexão de saudação.

> [!NOTE]
> Todos esses parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Digite um nome para a instância de Provance Olá que você deseja tooconnect com hello conector de gerenciamento de serviço de TI.  Use esse nome posteriormente no OMS quando você configurar os itens de trabalho nesse ITSM/exibir o Log Analytics detalhado. |
| **Selecionar Tipo de conexão**   | Selecione **Provance**. |
| **Nome de Usuário**   | Digite o nome de usuário de saudação que pode se conectar toohello conector de gerenciamento de serviço de TI.    |
| **Senha**   | Digite a senha Olá associada com este nome de usuário. **Observação:** nome de usuário e senha são usadas para gerar tokens de autenticação somente e não são armazenadas em qualquer lugar no serviço do OMS hello. _|
| **URL do Servidor**   | Digite a URL de saudação da sua instância de Provance que você deseja tooconnect tooIT conector do serviço de gerenciamento. |
| **ID do Cliente**   | Tipo hello ID do cliente para autenticar essa conexão, que é gerado em sua instância de Provance.  Para obter mais informações sobre a ID do cliente, consulte [como a autenticação do active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Escopo de Sincronização de Dados**   | Selecione itens de trabalho Provance Olá que você deseja tooOMS toosync, por meio de saudação conector de gerenciamento de serviço de TI.  Esses itens de trabalho são importados para o Log Analytics.   **Opções:** Incidentes, Solicitações de Alteração.|
| **Sincronizar Dados** | Digite hello número de dias anteriores a que você deseja que os dados de saudação do. **Limite máximo** 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se desejar que os itens de configuração de saudação toocreate produto ITSM da saudação. Quando selecionado, o OMS cria CIs Olá afetado como itens de configuração (no caso de CIs inexistente) Olá suportados sistema ITSM. **Padrão**: desabilitado.|

Quando conectado e sincronizado com êxito:

- Itens de trabalho selecionados da conexão Provance são importados para OMS **Log Analytics.**  Você pode exibir o resumo de saudação desses itens de trabalho no bloco do conector de gerenciamento de serviço de TI hello.
- Você pode criar incidentes e eventos de alertas do OMS ou pesquisa de Log nesta instância Provance.

Mais informações: [Criar itens de trabalho ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [Criar itens de trabalho ITSM de logs do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Conecte-se Cherwell tooIT conector de gerenciamento de serviço do OMS

Olá, seções a seguir fornecem detalhes sobre como tooconnect seu produto de Cherwell toohello conector de gerenciamento de serviço de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que ter Olá pré-requisitos atendidos a seguir:

- Conector de Gerenciamento do Serviço de TI instalado. Mais informações: [Configuração](log-analytics-itsmc-overview.md#configuration).
- ID do Cliente gerada. Mais informações: [Gerar a ID de cliente do Cherwell](#generate-client-id-for-cherwell).
- Função de usuário: Administrador.

### <a name="connection-procedure"></a>Procedimento de Conexão

Use Olá procedimento toocreate uma conexão Cherwell a seguir:

1. Vá muito**OMS** >  **configurações** > **fontes conectadas**.
2. Selecione **Conector ITSM,**  clique em **Adicionar Nova Conexão**.  

    ![Id de usuário do Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Fornecer informações de saudação conforme descrito em Olá a tabela a seguir e clique em **salvar** toocreate conexão de saudação.

> [!NOTE]
> Todos esses parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Digite um nome para a instância de Cherwell Olá que você deseja tooconnect toohello conector de gerenciamento de serviço de TI.  Use esse nome posteriormente no OMS quando você configurar os itens de trabalho nesse ITSM/exibir o Log Analytics detalhado. |
| **Selecionar Tipo de conexão**   | Selecione **Cherwell.** |
| **Nome de Usuário**   | Digite o nome de usuário de Cherwell de saudação que pode se conectar toohello conector de gerenciamento de serviço de TI. |
| **Senha**   | Digite a senha Olá associada com este nome de usuário. **Observação:** nome de usuário e senha são usadas para gerar tokens de autenticação somente e não são armazenadas em qualquer lugar no serviço do OMS hello.|
| **URL do Servidor**   | Digite a URL de saudação da sua instância do Cherwell que você deseja tooconnect tooIT conector do serviço de gerenciamento. |
| **ID do Cliente**   | Tipo hello ID do cliente para autenticar essa conexão, que é gerado em sua instância do Cherwell.   |
| **Escopo de Sincronização de Dados**   | Selecione itens de trabalho do Cherwell Olá que você deseja toosync por meio de saudação conector de gerenciamento de serviço de TI.  Esses itens de trabalho são importados para o Log Analytics.   **Opções:** Incidentes, Solicitações de Alteração. |
| **Sincronizar Dados** | Digite hello número de dias anteriores a que você deseja que os dados de saudação do. **Limite máximo** 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se desejar que os itens de configuração de saudação toocreate produto ITSM da saudação. Quando selecionado, o OMS cria CIs Olá afetado como itens de configuração (no caso de CIs inexistente) Olá suportados sistema ITSM. **Padrão**: desabilitado. |

Quando conectado e sincronizado com êxito:

- Selecionar trabalho itens dessa conexão Cherwell são importados para o Log Analytics do OMS. Você pode exibir o resumo de saudação desses itens de trabalho no bloco do conector de gerenciamento de serviço de TI hello.
- Você pode criar incidentes e eventos nesta instância do Cherwell do OMS. Mais informações: criar itens de trabalho ITSM para alertas do OMS e ITSM criar itens de trabalho de logs do OMS.

Mais informações: [Criar itens de trabalho ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [Criar itens de trabalho ITSM de logs do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Gerar a ID de Cliente do Cherwell

toogenerate hello chave/ID do cliente para Cherwell, use Olá procedimento a seguir:

1. Faça logon no tooyour Cherwell instância como administrador.
2. Clique em **Segurança** > **Editar configurações de cliente de API REST**.
3. Selecione **Criar novo cliente** > **segredo do cliente**.

    ![Id de usuário do Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Próximas etapas
 - [Criar itens de trabalho de ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Criar itens de trabalho de ITSM com base em logs do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Exibir a análise de log para sua conexão](log-analytics-itsmc-overview.md#using-the-solution)
