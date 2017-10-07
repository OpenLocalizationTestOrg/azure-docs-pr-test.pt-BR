---
title: "clusters de HDInsight domínio aaaManage - Azure | Microsoft Docs"
description: "Saiba como toomanage HDInsight domínio clusters"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Gerenciar clusters do HDInsight Ingressado no Domínio (Preview)
Saiba mais usuários hello e funções hello HDInsight ingressado no domínio, e como toomanage HDInsight domínio clusters.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Usuários dos clusters do HDInsight Ingressado no Domínio
Um cluster do HDInsight não está ingressado no domínio tem duas contas de usuário são criadas durante a criação do cluster hello:

* **Administração do Ambari**: essa conta também é conhecida como *usuário do Hadoop* ou *usuário HTTP*. Essa conta pode ser usado toolog em tooAmbari em https://&lt;clustername >. n e t. Ele também pode ser consultas toorun usadas em exibições do Ambari, executar trabalhos por meio de ferramentas externas (ou seja, do PowerShell, Templeton, Visual Studio) e autenticar com o driver de ODBC Hive hello e ferramentas de BI (ou seja, Excel, Power BI ou Tableau).
* **Usuário do SSH**: essa conta pode ser usada com o SSH e executar comandos sudo. Ela tem privilégios de raiz toohello VMs do Linux.

Um cluster de HDInsight domínio tem três novos usuários no usuário de administrador e SSH tooAmbari adição.

* **Administração de Ranger**: essa conta é a conta de administrador de Ranger Apache local do hello. Ela não é um usuário do Domínio do Active Directory. Essa conta pode ser usados toosetup políticas e tornar outros usuários administradores ou administradores delegados (para que os usuários possam gerenciar políticas). Por padrão, o nome de usuário de saudação é *admin* e a senha de saudação é Olá mesmo Olá a senha do administrador do Ambari. senha Olá pode ser atualizada na página de configurações de saudação em Ranger.
* **Usuário de domínio do administrador de cluster**: essa conta é um usuário de domínio do active directory designado como Olá administrador de cluster de Hadoop, incluindo Ambari e Ranger. Você deve fornecer as credenciais do usuário durante a criação do cluster. Este usuário tem Olá privilégios a seguir:

  * Ingressar em domínio de toohello máquinas e colocá-los em Olá UO que você especificar durante a criação do cluster.
  * Crie entidades de serviço dentro de saudação UO que você especificar durante a criação do cluster.
  * Criar entradas de DNS reverso.

    Saudação de Observação outros usuários do AD também tem esses privilégios.

    Há alguns pontos de extremidade em cluster hello (por exemplo, Templeton) que não são gerenciados pelo Ranger e, portanto, não são seguras. Esses pontos de extremidade são bloqueados para todos os usuários, exceto o usuário de domínio do administrador de cluster de saudação.
* **Regular**: durante a criação do cluster, você poderá fornecer vários grupos do Active Directory. usuários de saudação esses grupos serão sincronizado tooRanger e Ambari. Esses usuários são usuários do domínio e terão acesso tooonly gerenciados Ranger pontos de extremidade (por exemplo, Hiveserver2). Todas as políticas RBAC de hello e auditoria será usuários toothese aplicável.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Funções dos clusters do HDInsight Ingressado no Domínio
HDInsight domínio ter Olá funções a seguir:

* Administrador do cluster
* Operador do cluster
* Administrador de serviços
* Operador de serviço
* Usuário do cluster

**permissões de saudação toosee dessas funções**

1. Abra Olá Ambari da interface do usuário de gerenciamento.  Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).
2. No menu à esquerda do hello, clique em **funções**.
3. Clique em permissões de Olá Olá azul ponto de interrogação toosee:

    ![Permissões das funções do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Abrir Olá Ambari da interface do usuário de gerenciamento
1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Abra seu cluster do HDInsight em uma folha. Confira [Listar e mostrar clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Clique em **painel** da saudação menu superior tooopen Ambari.
4. Faça logon no tooAmbari usando a senha e nome de usuário de domínio do administrador de cluster hello.
5. Clique em Olá **Admin** menu suspenso no canto superior direito da saudação e clique **Ambari gerenciar**.

    ![Ambari gerenciado pelo HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Saudação da interface do usuário é semelhante a:

    ![Interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Lista de usuários de domínio Olá sincronizados do Active Directory
1. Abra Olá Ambari da interface do usuário de gerenciamento.  Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).
2. No menu à esquerda do hello, clique em **usuários**. Você deverá ver todos os usuários de saudação sincronizados do seu cluster de HDInsight toohello do Active Directory.

    ![Usuários listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Lista os grupos de domínio Olá sincronizados do Active Directory
1. Abra Olá Ambari da interface do usuário de gerenciamento.  Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).
2. No menu à esquerda do hello, clique em **grupos**. Você deverá ver todos os grupos de saudação sincronizados do seu cluster de HDInsight toohello do Active Directory.

    ![Grupos listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Configurar permissões de exibições do Hive
1. Abra Olá Ambari da interface do usuário de gerenciamento.  Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).
2. No menu à esquerda do hello, clique em **exibições**.
3. Clique em **HIVE** tooshow detalhes de saudação.

    ![Exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Clique em Olá **exibição Hive** link tooconfigure Hive exibições.
5. Role para baixo toohello **permissões** seção.

    ![Permissões de configuração das exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Clique em **adicionar usuário** ou **adicionar grupo**e, em seguida, especifique Olá usuários ou grupos podem usar exibições do Hive.

## <a name="configure-users-for-hello-roles"></a>Configurar usuários para funções hello
 toosee uma lista de funções e suas permissões, consulte [clusters HDInsight funções de domínio](#roles-of-domain---joined-hdinsight-clusters).

1. Abra Olá Ambari da interface do usuário de gerenciamento.  Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).
2. No menu à esquerda do hello, clique em **funções**.
3. Clique em **adicionar usuário** ou **adicionar grupo** tooassign usuários e grupos de funções de toodifferent.

## <a name="next-steps"></a>Próximas etapas
* Para configurar um cluster do HDInsight ingressado no domínio, confira [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurar clusters do HDInsight Ingressado no Domínio).
* Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).
* Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
