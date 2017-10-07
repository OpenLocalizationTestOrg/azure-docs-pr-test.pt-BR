---
title: "aaaConfigure políticas de Hive no HDInsight domínio - Azure | Microsoft Docs"
description: Saiba como...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Configurar políticas do Hive no HDInsight associado ao domínio (Visualização)
Saiba como as políticas de Ranger Apache tooconfigure para o Hive. Neste artigo, você deve criar dois Ranger políticas toorestrict acesso toohello hivesampletable. Olá hivesampletable vem com clusters HDInsight. Depois que você configurou políticas hello, você usar tabelas de tooHive do Excel e ODBC driver tooconnect no HDInsight.

## <a name="prerequisites"></a>Pré-requisitos
* Um cluster HDInsight associado a um domínio. Confira [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md).
* Uma estação de trabalho com Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.

## <a name="connect-tooapache-ranger-admin-ui"></a>Conecte-se tooApache Ranger da interface do usuário de administrador
**tooconnect tooRanger Admin UI**

1. Em um navegador, conecte-se tooRanger Admin UI. Olá URL é https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > O Ranger usa credenciais diferentes das do cluster Hadoop. navegadores tooprevent usando credenciais armazenadas em cache do Hadoop, use toohello de tooconnect nova janela de navegador inprivate Ranger da interface do usuário de administrador.
   >
   >
2. Faça logon usando a senha e nome de usuário de domínio do administrador de cluster hello:

    ![Home page do Ranger associado ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Atualmente, o Ranger só funciona com o Hive e o Yarn.

## <a name="create-domain-users"></a>Criar usuários de Domínio
Em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), você criou hiveruser1 e hiveuser2. Você usará a conta de usuário de dois Olá neste tutorial.

## <a name="create-ranger-policies"></a>Criar políticas do Ranger
Nesta seção, você criará duas políticas do Ranger para acessar hivesampletable. Você pode dar permissão select em um conjunto diferente de colunas. Ambos os usuários foram criados em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).  Na próxima seção, Olá, você testará duas políticas Olá no Excel.

**políticas de Ranger toocreate**

1. Abrir a Interface de Usuário de Administração do Ranger. Consulte [conectar tooApache Ranger da interface do usuário de administrador](#connect-to-apache-ranager-admin-ui).
2. Clique em **&lt;ClusterName >_hive**, em **Hive**. Você deverá ver duas políticas de pré-configuração.
3. Clique em **adicionar nova política**e, em seguida, digite Olá valores a seguir:

   * Nome da política: read-hivesampletable-all
   * Hive de Banco de Dados: padrão
   * tabela: hivesampletable
   * Coluna de hive: *
   * Selecione o usuário: hiveuser1
   * Permissões: selecionar

     ![Configurar política do Hive do Ranger associada ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Se um usuário de domínio não é populado em Selecionar usuário, aguarde alguns instantes para toosync Ranger com o AAD.
     >
     >
4. Clique em **adicionar** toosave política de saudação.
5. Repita Olá duas últimas etapas toocreate outra política com hello propriedades a seguir:

   * Nome da política: read-hivesampletable-devicemake
   * Hive de Banco de Dados: padrão
   * tabela: hivesampletable
   * Coluna do hive: clientid, devicemake
   * Selecione o usuário: hiveuser2
   * Permissões: selecionar

## <a name="create-hive-odbc-data-source"></a>Criar uma fonte de dados ODBC do Hive
Olá instruções podem ser encontradas no [fonte de dados ODBC de Hive criar](hdinsight-connect-excel-hive-odbc-driver.md).  

    Propriedade|Descrição
    ---|---
    Nome da fonte de dados|Dê uma fonte de dados do nome tooyour
    Host|Digite &lt;HDInsightClusterName>.azurehdinsight.net. Por exemplo, meu_Cluster_HDI.azurehdinsight.net
    Port|Use <strong>443</strong>. (Essa porta foi alterada de 563 too443.)
    Banco de dados|Use <strong>Padrão</strong>.
    Tipo de servidor Hive|Selecione <strong>Servidor Hive 2</strong>
    Mecanismo|Selecione <strong>Serviço do Azure HDInsight</strong>
    Caminho HTTP|Deixe em branco.
    Nome de usuário|Digite hiveuser1@contoso158.onmicrosoft.com. Atualize o nome de domínio de saudação se ele for diferente.
    Senha|Insira a senha de saudação para hiveuser1.
    </table>

Certifique-se de que tooclick **teste** antes de salvar a fonte de dados de saudação.

## <a name="import-data-into-excel-from-hdinsight"></a>Importar dados do HDInsight para o Excel
Na seção de última hello, você configurou duas políticas.  hiveuser1 tem Olá permissão em todas as colunas de saudação select e hiveuser2 tem Olá permissão select na duas colunas. Nesta seção, você pode representar Olá dois usuários tooimport dados no Excel.

1. Abra uma pasta de trabalho nova ou existente no Excel.
2. De saudação **dados** , clique em **de outras fontes de dados**e, em seguida, clique em **do Assistente de Conexão de dados** toolaunch Olá **,AssistentedeConexãodedados**.

    ![Assistente de conexão de dados][img-hdi-simbahiveodbc.excel.dataconnection]
3. Selecione **DSN ODBC** como fonte de dados hello e clique **próximo**.
4. De fontes de dados ODBC, Olá Selecionar fonte de dados nome que você criou na etapa anterior hello e, em seguida, clique em **próximo**.
5. Digite novamente a senha Olá para cluster Olá no Assistente de saudação e, em seguida, clique em **Okey**. Aguarde a saudação **Selecionar banco de dados e tabela** tooopen da caixa de diálogo. Isso pode levar alguns segundos.
6. Selecione **hivesampletable** e clique em **Avançar**.
7. Clique em **Concluir**.
8. Em Olá **importar dados** caixa de diálogo, você pode alterar ou especificar Olá consulta. toodo, clique em **propriedades**. Isso pode levar alguns segundos.
9. Clique em Olá **definição** na guia texto do comando de saudação é:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Por políticas de Ranger Olá definidos, hiveuser1 tem permissão select em todas as colunas de saudação.  Então, essa consulta funciona com as credenciais de hiveuser1, mas não funciona com as credenciais de hiveuser2.

   ![Propriedades de conexão][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Clique em **Okey** caixa de diálogo de propriedades de Conexão de saudação tooclose.
11. Clique em **Okey** tooclose Olá **importar dados** caixa de diálogo.  
12. Redigite a senha de saudação para hiveuser1 e, em seguida, clique em **Okey**. Levará alguns segundos antes de dados obtém tooExcel importado. Quando estiver pronto, você deverá ver 11 colunas de dados.

política do tootest Olá segundo (leitura-hivesampletable-devicemake) que você criou na seção de última Olá

1. Adicione uma nova planilha no Excel.
2. Siga a dados do hello último procedimento tooimport Olá.  alteração somente Hello, que você fará é credenciais do toouse hiveuser2 em vez do hiveuser1. Isso irá falhar porque hiveuser2 tem apenas duas colunas de toosee de permissão. Você deve obter Olá erro a seguir:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Siga Olá mesmo dados de tooimport de procedimento. Neste momento, usar credenciais do hiveuser2 e também modificar a instrução select hello from:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    para:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Quando estiver pronto, você deverá ver duas colunas de dados importados.

## <a name="next-steps"></a>Próximas etapas
* Para configurar um cluster HDInsight associado a um domínio, confira [Configurar clusters HDInsight associados a domínio](hdinsight-domain-joined-configure.md).
* Para gerenciar um cluster HDInsight associado a um domínio, confira [Gerenciar clusters HDInsight associados a domínio](hdinsight-domain-joined-manage.md).
* Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Para conectar-se de Hive usando JDBC Hive, consulte [conectar tooHive no Azure HDInsight usando Olá Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)
* Para conectar tooHadoop do Excel usando o ODBC Hive, consulte [tooHadoop Excel conectar-se com hello unidade Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)
* Para conectar usando o Power Query do Excel tooHadoop, consulte [tooHadoop Excel se conectar usando o Power Query](hdinsight-connect-excel-power-query.md)
