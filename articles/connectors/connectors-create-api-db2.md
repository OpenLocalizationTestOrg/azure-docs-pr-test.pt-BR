---
title: "conector de saudação DB2 aaaAdd em seus aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do DB2 com parâmetros da API REST"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Introdução ao conector do DB2 Olá
Conector da Microsoft para DB2 se conecta a aplicativos lógicos tooresources armazenados em um banco de dados IBM DB2. Esse conector inclui um toocommunicate de cliente da Microsoft com computadores remotos servidores DB2 através de uma rede TCP/IP. Isso inclui bancos de dados de nuvem, como IBM Bluemix dashDB ou IBM DB2 para Windows em execução no Azure virtualização e bancos de dados usando o gateway de dados local Olá local. Consulte Olá [suporte lista](connectors-create-api-db2.md#supported-db2-platforms-and-versions) de plataformas IBM DB2 e as versões (neste tópico).

conector Olá DB2 oferece suporte a saudação operações de banco de dados a seguir:

* Listar tabelas do banco de dados
* Ler uma linha usando SELECT
* Ler todas as linhas usando SELECT
* Adicionar uma linha usando INSERT
* Alterar uma linha usando UPDATE
* Remover uma linha usando DELETE

Este tópico mostra como conector de saudação toouse em um tooprocess do aplicativo de lógica de banco de dados operações.

toolearn mais sobre aplicativos lógicos, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Ações disponíveis
conector Olá DB2 oferece suporte a saudação ações de lógica de aplicativo a seguir:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Listar tabelas
Criar um aplicativo lógico para qualquer operação é composta de muitas etapas executadas por meio do portal do Microsoft Azure hello.

No aplicativo de lógica de saudação, você pode adicionar tabelas de toolist uma ação em um banco de dados do DB2. Olá ação instrui a declaração de esquema do hello conector tooprocess um DB2, como `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `Db2getTables`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, defina Olá **Intervalo** tootype **7**.  
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite `db2` em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - obter tabelas (visualização)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. Em Olá **DB2 - obter tabelas** painel de configuração, selecione **caixa de seleção** tooenable **conectar por meio do gateway de dados no local**. Observe que alterar configurações de saudação de nuvem tooon locais.
   
   * Digite o valor para **Server**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `ibmserver01:50000`.
   * Digite o valor para o **Banco de Dados**. Por exemplo, digite `nwind`.
   * Selecione o valor para a **Autenticação**. Por exemplo, selecione **Básica**.
   * Digite o valor para o **Nome de Usuário**. Por exemplo, digite `db2admin`.
   * Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
   * Selecione o valor para o **Gateway**. Por exemplo, selecione **datagateway01**.
7. Selecione **Criar** e, em seguida, **Salvar**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. Em Olá **Db2getTables** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
9. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_tables**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir uma lista de tabelas.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Criar conexões de saudação
Esse conector dá suporte a conexões toodatabases hospedado localmente e na nuvem hello usando Olá seguintes propriedades de conexão. 

| Propriedade | Descrição |
| --- | --- |
| Servidor |Obrigatório. Aceita um valor da cadeia de caracteres que representa um endereço TCP/IP ou alias no formato IPv4 ou IPv6, seguido de (delimitado por dois pontos) um número de porta TCP/IP. |
| Banco de Dados |Obrigatório. Aceita um valor da cadeia de caracteres que representa um Nome do Banco de Dados Relacional (RDBNAM) DRDA. O DB2 para z/OS aceita uma cadeia de caracteres de 16 bytes (o banco de dados é conhecido como um IBM DB2 para o local do z/OS). O DB2 para i5/OS aceita uma cadeia de caracteres de 18 bytes (o banco de dados é conhecido como um IBM DB2 para o banco de dados relacional i). O DB2 para LUW aceita uma cadeia de caracteres de 8 bytes. |
| Autenticação |Opcional. Aceita um valor de item de lista, Básica ou Windows (kerberos). |
| Nome de Usuário |Obrigatório. Aceita um valor de cadeia de caracteres. O DB2 para z/OS aceita uma cadeia de caracteres de 8 bytes. O DB2 para i aceita uma cadeia de caracteres de 10 bytes. O DB2 para Linux ou UNIX aceita uma cadeia de caracteres de 8 bytes. O DB2 para Windows aceita uma cadeia de caracteres de 30 bytes. |
| Senha |Obrigatório. Aceita um valor de cadeia de caracteres. |
| Gateway |Obrigatório. Aceita um valor de item de lista, que representa a saudação local dados gateway definido tooLogic aplicativos no grupo de armazenamento de saudação. |

## <a name="create-hello-on-premises-gateway-connection"></a>Criar conexão de gateway de saudação local
Esse conector pode acessar um banco de dados local DB2 usando Olá local gateway. Consulte os tópicos do gateway para obter mais informações. 

1. Em Olá **Gateways** painel de configuração, selecione **caixa de seleção** tooenable **conectar por meio do gateway**. Observe que alterar configurações de saudação de nuvem tooon locais.
2. Digite o valor para **Server**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `ibmserver01:50000`.
3. Digite o valor para o **Banco de Dados**. Por exemplo, digite `nwind`.
4. Selecione o valor para a **Autenticação**. Por exemplo, selecione **Básica**.
5. Digite o valor para o **Nome de Usuário**. Por exemplo, digite `db2admin`.
6. Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
7. Selecione o valor para o **Gateway**. Por exemplo, selecione **datagateway01**.
8. Selecione **criar** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Criar conexão de nuvem Olá
Este conector pode acessar um banco de dados DB2 de nuvem. 

1. Em Olá **Gateways** painel de configuração, deixe Olá **caixa de seleção** desabilitado (clicados) **conectar por meio do gateway**. 
2. Digite o valor para o **Nome da conexão**. Por exemplo, digite `hisdemo2`.
3. Digite o valor para **nome do servidor DB2**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `hisdemo2.cloudapp.net:50000`.
4. Digite o valor para o **Nome do banco de dados DB2**. Por exemplo, digite `nwind`.
5. Digite o valor para o **Nome de Usuário**. Por exemplo, digite `db2admin`.
6. Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
7. Selecione **criar** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Buscar todas as linhas usando SELECT
Você pode definir um toofetch de ação do aplicativo lógica todas as linhas em uma tabela DB2. Isso instrui Olá conector tooprocess uma instrução SELECT de DB2, como `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `Db2getRows`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite `db2` em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - Get linhas (visualização)**.
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**.
7. Em Olá **conexões** painel de configuração, selecione **criar novo**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. Em Olá **Gateways** painel de configuração, deixe Olá **caixa de seleção** desabilitado (clicados) **conectar por meio do gateway**.
   
   * Digite o valor para o **Nome da conexão**. Por exemplo, digite `HISDEMO2`.
   * Digite o valor para **nome do servidor DB2**, na forma de saudação do endereço ou alias de número de porta de dois-pontos. Por exemplo, digite `HISDEMO2.cloudapp.net:50000`.
   * Digite o valor para o **Nome do banco de dados DB2**. Por exemplo, digite `NWIND`.
   * Digite o valor para o **Nome de Usuário**. Por exemplo, digite `db2admin`.
   * Digite o valor para a **Senha**. Por exemplo, digite `Password1`.
9. Selecione **criar** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
11. Opcionalmente, selecione **Mostrar opções avançadas** toospecify opções de consulta.
12. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. Em Olá **Db2getRows** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
14. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir uma lista de linhas.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Adicionar uma linha usando INSERT
Você pode definir uma lógica aplicativo ação tooadd uma linha em uma tabela DB2. Essa ação instrui Olá conector tooprocess uma instrução INSERT do DB2, como `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `Db2insertRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **db2** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - linha de inserção (visualização)**.
6. Em Olá **DB2 - linha de inserção (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel de configuração, selecione uma conexão. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**, digite `Area 99999` e digite `102` para **REGIONID**. 
10. Selecione **Salvar**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. Em Olá **Db2insertRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a nova linha de saudação.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Buscar uma linha usando SELECT
Você pode definir uma lógica aplicativo ação toofetch uma linha em uma tabela DB2. Essa ação instrui Olá conector tooprocess uma instrução Selecionar onde do DB2, como `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome** (por exemplo, "**Db2getRow**"), **Assinatura**, **Grupo de recursos**,**Local** e **Plano do Serviço de Aplicativo**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista. 
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **db2** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - Get linhas (visualização)**.
6. Em Olá **obter linhas (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**. 
10. Opcionalmente, selecione **Mostrar opções avançadas** toospecify opções de consulta.
11. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. Em Olá **Db2getRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
13. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a linha.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Alterar uma linha usando UPDATE
Você pode definir uma lógica aplicativo ação toochange uma linha em uma tabela DB2. Essa ação instrui Olá conector tooprocess uma instrução UPDATE do DB2, como `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `Db2updateRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista.
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, digite **db2** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - linha de atualização (visualização)**.
6. Em Olá **DB2 - linha de atualização (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione tooselect uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**, digite `Updated 99999` e digite `102` para **REGIONID**. 
10. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. Em Olá **Db2updateRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a nova linha de saudação.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Remover uma linha usando DELETE
Você pode definir uma lógica aplicativo ação tooremove uma linha em uma tabela DB2. Essa ação instrui Olá conector tooprocess uma instrução DELETE do DB2, como `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Criar um aplicativo lógico
1. Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.
2. Digite hello **nome**, como `Db2deleteRow`, **assinatura**, **grupo de recursos**, **local**, e **aplicativo Plano de serviço**. Selecione **Pin toodashboard**e, em seguida, selecione **criar**.

### <a name="add-a-trigger-and-action"></a>Adicionar um gatilho e uma ação
1. Em Olá **lógica aplicativos Designer**, selecione **LogicApp em branco** em Olá **modelos** lista. 
2. Em Olá **gatilhos** lista, selecione **recorrência**. 
3. Em Olá **recorrência** gatilho, selecione **editar**, selecione **frequência** suspensa tooselect **dia**e, em seguida, selecione  **Intervalo de** tootype **7**. 
4. Selecione Olá **+ nova etapa** caixa e, em seguida, selecione **adicionar uma ação**.
5. Em Olá **ações** lista, selecione **db2** em Olá **procurar mais ações** caixa de edição e, em seguida, selecione **DB2 - Excluir linha (visualização)**.
6. Em Olá **DB2 - Excluir linha (visualização)** ação, selecione **alterar conexão**. 
7. Em Olá **conexões** painel configurações, selecione uma conexão existente. Por exemplo, selecione **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Em Olá **nome de tabela** lista, selecione Olá **a seta para baixo**e, em seguida, selecione **área**.
9. Insira valores para todas as colunas necessárias (confira o asterisco vermelho). Por exemplo, digite `99999` para **AREAID**. 
10. Selecione **Salvar**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. Em Olá **Db2deleteRow** folha, dentro de saudação **todas as execuções** lista sob **resumo**, selecione Olá item listado primeiro (execução mais recente).
12. Em Olá **aplicativo lógico executar** folha, selecione **detalhes da execução**. Dentro de saudação **ação** lista, selecione **Get_rows**. Consultar valor Olá **Status**, que deve ser **êxito**. Selecione Olá **link entradas** tooview entradas de saudação. Selecione Olá **saídas link**e saídas de saudação do modo de exibição; que deve incluir a linha hello excluído.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Plataformas e versões com suporte do DB2
Esse conector dá suporte a saudação plataformas IBM DB2 e versões, bem como produtos IBM DB2 compatíveis (por exemplo, IBM Bluemix dashDB) que dão suporte ao banco de dados arquitetura DRDA (Distributed Relational) SQL Access Manager (SQLAM) versão 10 e 11 a seguir:

* IBM DB2 para z/OS 11.1
* IBM DB2 para z/OS 10.1
* IBM DB2 para i 7.3
* IBM DB2 para i 7.2
* IBM DB2 para i 7.1
* IBM DB2 para LUW 11
* IBM DB2 para LUW 10.5

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/db2/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).

