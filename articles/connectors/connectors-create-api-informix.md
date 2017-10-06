---
title: "conector de Informix Olá aaaAdd em seus aplicativos lógicos | Microsoft Docs"
description: "Visão geral do Conector do Informix com os parâmetros da API REST"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Introdução ao conector do hello Informix
Conector da Microsoft para Informix conecta aplicativos lógicos tooresources armazenados em um banco de dados do IBM Informix. conector do Informix Olá abrange um Microsoft toocommunicate tooremote Informix servidor os computadores cliente em uma rede TCP/IP. Isso inclui bancos de dados de nuvem, como IBM Informix para Windows em execução no Azure virtualização e bancos de dados usando o gateway de dados local Olá local. Consulte Olá [suporte lista](connectors-create-api-informix.md#supported-informix-platforms-and-versions) do IBM Informix plataformas e versões (neste tópico).

conector de saudação dá suporte a saudação operações de banco de dados a seguir:

* Listar tabelas do banco de dados
* Ler uma linha usando SELECT
* Ler todas as linhas usando SELECT
* Adicionar uma linha usando INSERT
* Alterar uma linha usando UPDATE
* Remover uma linha usando DELETE

Este tópico mostra como conector de saudação toouse em um tooprocess do aplicativo de lógica de banco de dados operações.

toolearn mais sobre aplicativos lógicos, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Ações disponíveis
Esse conector dá suporte a saudação ações de lógica de aplicativo a seguir:

* Getables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Listar tabelas
Criar um aplicativo lógico para qualquer operação é composta de muitas etapas executadas por meio do portal do Microsoft Azure hello.

No aplicativo de lógica de saudação, você pode adicionar tabelas de toolist uma ação em um banco de dados Informix. Essa ação instrui Olá conector tooprocess uma declaração de esquema Informix, como `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `InformixgetTables`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**.  
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - obter tabelas (visualização)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. Em Olá **Informix - obter tabelas** painel de configuração, selecione **caixa de seleção** tooenable **conectar por meio do gateway de dados no local**. Observe que alterar configurações de saudação de nuvem tooon locais.
   
   * Digite o valor para **Server**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `ibmserver01:9089`.
   * Digite o valor para o **Banco de Dados**. Por exemplo, digite `nwind`.
   * Selecione o valor para a **Autenticação**. Por exemplo, selecione **Básica**.
   * Digite o valor para o **Nome de Usuário**. Por exemplo, digite `informix`.
   * Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
   * Selecione o valor para o **Gateway**. Por exemplo, selecione **datagateway01**.
7. Selecione **Criar** e, em seguida, **Salvar**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. Em Olá **InformixgetTables** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
9. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_tables**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir uma lista de tabelas.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Criar conexões de saudação
Esse conector dá suporte a conexões toodatabase locais e na nuvem hello usando Olá seguintes propriedades de conexão. 

| Propriedade | Descrição |
| --- | --- |
| Servidor |Obrigatório. Aceita um valor da cadeia de caracteres que representa um endereço TCP/IP ou alias no formato IPv4 ou IPv6, seguido de (delimitado por dois pontos) um número de porta TCP/IP. |
| Banco de Dados |Obrigatório. Aceita um valor da cadeia de caracteres que representa um Nome do Banco de Dados Relacional (RDBNAM) DRDA. O Informix aceita uma cadeia de caracteres de 128 bytes (o banco de dados é conhecido como um nome de banco de dados IBM Informix (dbname)). |
| Autenticação |Opcional. Aceita um valor de item de lista, Básica ou Windows (kerberos). |
| Nome de Usuário |Obrigatório. Aceita um valor de cadeia de caracteres. |
| Senha |Obrigatório. Aceita um valor de cadeia de caracteres. |
| Gateway |Obrigatório. Aceita um valor de item de lista, que representa a saudação local dados gateway definido tooLogic aplicativos no grupo de armazenamento de saudação. |

## <a name="create-hello-on-premises-gateway-connection"></a>Criar conexão de gateway de saudação local
Esse conector pode acessar um banco de dados local Informix usando o gateway de dados local hello. Consulte os tópicos do gateway para obter mais informações. 

1. Em Olá **Gateways** painel de configuração, selecione **caixa de seleção** tooenable **conectar por meio do gateway**. Consulte Olá alterar configurações de nuvem tooon locais.
2. Digite o valor para **Server**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `ibmserver01:9089`.
3. Digite o valor para o **Banco de Dados**. Por exemplo, digite `nwind`.
4. Selecione o valor para a **Autenticação**. Por exemplo, selecione **Básica**.
5. Digite o valor para o **Nome de Usuário**. Por exemplo, digite `informix`.
6. Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
7. Selecione o valor para o **Gateway**. Por exemplo, selecione **datagateway01**.
8. Selecione **criar** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Criar conexão de nuvem Olá
Este conector pode acessar uma nuvem de banco de dados Informix. 

1. Em Olá **Gateways** painel de configuração, deixe Olá **caixa de seleção** desabilitado (clicados) **conectar por meio do gateway**. 
2. Digite o valor para o **Nome da conexão**. Por exemplo, digite `hisdemo2`.
3. Digite o valor para **nome do servidor Informix**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `hisdemo2.cloudapp.net:9089`.
4. Digite o valor para **nome do banco de dados Informix**. Por exemplo, digite `nwind`.
5. Digite o valor para o **Nome de Usuário**. Por exemplo, digite `informix`.
6. Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
7. Selecione **criar** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Buscar todas as linhas usando SELECT
Você pode criar um toofetch de ação do aplicativo lógica todas as linhas na tabela de Informix hello. Essa ação instrui Olá conector tooprocess uma instrução SELECT do Informix, como `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome** (por exemplo, "**InformixgetRows**"), **Assinatura**, **Grupo de recursos**, **Local** e **Plano do Serviço de Aplicativo**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - Get linhas (visualização)** .
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**.
7. Em Olá **conexões** painel de configuração, selecione **criar novo**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. Em Olá **Gateways** painel de configuração, deixe Olá **caixa de seleção** desabilitado (clicados) **conectar por meio do gateway**.
   
   * Digite o valor para o **Nome da conexão**. Por exemplo, digite `HISDEMO2`.
   * Digite o valor para **nome do servidor Informix**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `HISDEMO2.cloudapp.net:9089`.
   * Digite o valor para **nome do banco de dados Informix**. Por exemplo, digite `NWIND`.
   * Digite o valor para o **Nome de Usuário**. Por exemplo, digite `informix`.
   * Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
9. Selecione **criar** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
11. Opcionalmente, selecione **Mostrar opções avançadas** toospecify opções de consulta.
12. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. Em Olá **InformixgetRows** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
14. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir uma lista de linhas.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Adicionar uma linha usando INSERT
Você pode criar uma lógica aplicativo ação tooadd uma linha em uma tabela Informix. Essa ação instrui Olá conector tooprocess uma instrução INSERT Informix, como `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `InformixinsertRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - linha de inserção (visualização)**.
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel de configuração, selecione tooselect uma conexão. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**, digite `Area 99999` e digite `102` para **REGIONID**. 
10. Selecione **Salvar**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. Em Olá **InformixinsertRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a nova linha de saudação.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Buscar uma linha usando SELECT
Você pode criar uma lógica aplicativo ação toofetch uma linha em uma tabela Informix. Essa ação instrui Olá conector tooprocess uma instrução Selecionar onde do Informix, como `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `InformixgetRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - Get linhas (visualização)** .
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione tooselect uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**. 
10. Opcionalmente, selecione **Mostrar opções avançadas** toospecify opções de consulta.
11. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. Em Olá **InformixgetRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
13. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a linha.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Alterar uma linha usando UPDATE
Você pode criar uma lógica aplicativo ação toochange uma linha em uma tabela Informix. Essa ação instrui Olá conector tooprocess uma instrução UPDATE Informix, como `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `InformixupdateRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - linha de atualização (visualização)**.
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione tooselect uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**, digite `Updated 99999` e digite `102` para **REGIONID**. 
10. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. Em Olá **InformixupdateRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a nova linha de saudação.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Remover uma linha usando DELETE
Você pode criar uma lógica aplicativo ação tooremove uma linha em uma tabela Informix. Essa ação instrui Olá conector tooprocess uma instrução DELETE do Informix, como `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `InformixdeleteRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **informix** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **Informix - Excluir linha (visualização)**.
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**. 
10. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. Em Olá **InformixdeleteRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a linha hello excluído.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Versões e plataformas Informix com suporte
Esse conector dá suporte a saudação seguintes versões do IBM Informix, quando configurado conexões de cliente toosupport DRDA Distributed Relational Database Architecture ().

* IBM Informix 12.1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/informix/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).

