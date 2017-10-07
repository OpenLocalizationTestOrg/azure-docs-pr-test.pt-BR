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
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="1db86-103">Gerenciar clusters do HDInsight Ingressado no Domínio (Preview)</span><span class="sxs-lookup"><span data-stu-id="1db86-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="1db86-104">Saiba mais usuários hello e funções hello HDInsight ingressado no domínio, e como toomanage HDInsight domínio clusters.</span><span class="sxs-lookup"><span data-stu-id="1db86-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="1db86-105">Usuários dos clusters do HDInsight Ingressado no Domínio</span><span class="sxs-lookup"><span data-stu-id="1db86-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="1db86-106">Um cluster do HDInsight não está ingressado no domínio tem duas contas de usuário são criadas durante a criação do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="1db86-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="1db86-107">**Administração do Ambari**: essa conta também é conhecida como *usuário do Hadoop* ou *usuário HTTP*.</span><span class="sxs-lookup"><span data-stu-id="1db86-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="1db86-108">Essa conta pode ser usado toolog em tooAmbari em https://&lt;clustername >. n e t.</span><span class="sxs-lookup"><span data-stu-id="1db86-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="1db86-109">Ele também pode ser consultas toorun usadas em exibições do Ambari, executar trabalhos por meio de ferramentas externas (ou seja, do PowerShell, Templeton, Visual Studio) e autenticar com o driver de ODBC Hive hello e ferramentas de BI (ou seja, Excel, Power BI ou Tableau).</span><span class="sxs-lookup"><span data-stu-id="1db86-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="1db86-110">**Usuário do SSH**: essa conta pode ser usada com o SSH e executar comandos sudo.</span><span class="sxs-lookup"><span data-stu-id="1db86-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="1db86-111">Ela tem privilégios de raiz toohello VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="1db86-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="1db86-112">Um cluster de HDInsight domínio tem três novos usuários no usuário de administrador e SSH tooAmbari adição.</span><span class="sxs-lookup"><span data-stu-id="1db86-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="1db86-113">**Administração de Ranger**: essa conta é a conta de administrador de Ranger Apache local do hello.</span><span class="sxs-lookup"><span data-stu-id="1db86-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="1db86-114">Ela não é um usuário do Domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db86-114">It is not an active directory domain user.</span></span> <span data-ttu-id="1db86-115">Essa conta pode ser usados toosetup políticas e tornar outros usuários administradores ou administradores delegados (para que os usuários possam gerenciar políticas).</span><span class="sxs-lookup"><span data-stu-id="1db86-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="1db86-116">Por padrão, o nome de usuário de saudação é *admin* e a senha de saudação é Olá mesmo Olá a senha do administrador do Ambari.</span><span class="sxs-lookup"><span data-stu-id="1db86-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="1db86-117">senha Olá pode ser atualizada na página de configurações de saudação em Ranger.</span><span class="sxs-lookup"><span data-stu-id="1db86-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="1db86-118">**Usuário de domínio do administrador de cluster**: essa conta é um usuário de domínio do active directory designado como Olá administrador de cluster de Hadoop, incluindo Ambari e Ranger.</span><span class="sxs-lookup"><span data-stu-id="1db86-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="1db86-119">Você deve fornecer as credenciais do usuário durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="1db86-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="1db86-120">Este usuário tem Olá privilégios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1db86-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="1db86-121">Ingressar em domínio de toohello máquinas e colocá-los em Olá UO que você especificar durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="1db86-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="1db86-122">Crie entidades de serviço dentro de saudação UO que você especificar durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="1db86-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="1db86-123">Criar entradas de DNS reverso.</span><span class="sxs-lookup"><span data-stu-id="1db86-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="1db86-124">Saudação de Observação outros usuários do AD também tem esses privilégios.</span><span class="sxs-lookup"><span data-stu-id="1db86-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="1db86-125">Há alguns pontos de extremidade em cluster hello (por exemplo, Templeton) que não são gerenciados pelo Ranger e, portanto, não são seguras.</span><span class="sxs-lookup"><span data-stu-id="1db86-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="1db86-126">Esses pontos de extremidade são bloqueados para todos os usuários, exceto o usuário de domínio do administrador de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1db86-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="1db86-127">**Regular**: durante a criação do cluster, você poderá fornecer vários grupos do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db86-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="1db86-128">usuários de saudação esses grupos serão sincronizado tooRanger e Ambari.</span><span class="sxs-lookup"><span data-stu-id="1db86-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="1db86-129">Esses usuários são usuários do domínio e terão acesso tooonly gerenciados Ranger pontos de extremidade (por exemplo, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="1db86-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="1db86-130">Todas as políticas RBAC de hello e auditoria será usuários toothese aplicável.</span><span class="sxs-lookup"><span data-stu-id="1db86-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="1db86-131">Funções dos clusters do HDInsight Ingressado no Domínio</span><span class="sxs-lookup"><span data-stu-id="1db86-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="1db86-132">HDInsight domínio ter Olá funções a seguir:</span><span class="sxs-lookup"><span data-stu-id="1db86-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="1db86-133">Administrador do cluster</span><span class="sxs-lookup"><span data-stu-id="1db86-133">Cluster Administrator</span></span>
* <span data-ttu-id="1db86-134">Operador do cluster</span><span class="sxs-lookup"><span data-stu-id="1db86-134">Cluster Operator</span></span>
* <span data-ttu-id="1db86-135">Administrador de serviços</span><span class="sxs-lookup"><span data-stu-id="1db86-135">Service Administrator</span></span>
* <span data-ttu-id="1db86-136">Operador de serviço</span><span class="sxs-lookup"><span data-stu-id="1db86-136">Service Operator</span></span>
* <span data-ttu-id="1db86-137">Usuário do cluster</span><span class="sxs-lookup"><span data-stu-id="1db86-137">Cluster User</span></span>

<span data-ttu-id="1db86-138">**permissões de saudação toosee dessas funções**</span><span class="sxs-lookup"><span data-stu-id="1db86-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="1db86-139">Abra Olá Ambari da interface do usuário de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1db86-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="1db86-140">Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="1db86-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="1db86-141">No menu à esquerda do hello, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="1db86-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="1db86-142">Clique em permissões de Olá Olá azul ponto de interrogação toosee:</span><span class="sxs-lookup"><span data-stu-id="1db86-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![Permissões das funções do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="1db86-144">Abrir Olá Ambari da interface do usuário de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="1db86-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="1db86-145">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1db86-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1db86-146">Abra seu cluster do HDInsight em uma folha.</span><span class="sxs-lookup"><span data-stu-id="1db86-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="1db86-147">Confira [Listar e mostrar clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="1db86-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="1db86-148">Clique em **painel** da saudação menu superior tooopen Ambari.</span><span class="sxs-lookup"><span data-stu-id="1db86-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="1db86-149">Faça logon no tooAmbari usando a senha e nome de usuário de domínio do administrador de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1db86-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="1db86-150">Clique em Olá **Admin** menu suspenso no canto superior direito da saudação e clique **Ambari gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="1db86-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![Ambari gerenciado pelo HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="1db86-152">Saudação da interface do usuário é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="1db86-152">hello UI looks like:</span></span>

    ![Interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="1db86-154">Lista de usuários de domínio Olá sincronizados do Active Directory</span><span class="sxs-lookup"><span data-stu-id="1db86-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="1db86-155">Abra Olá Ambari da interface do usuário de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1db86-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="1db86-156">Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="1db86-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="1db86-157">No menu à esquerda do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="1db86-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="1db86-158">Você deverá ver todos os usuários de saudação sincronizados do seu cluster de HDInsight toohello do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db86-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Usuários listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="1db86-160">Lista os grupos de domínio Olá sincronizados do Active Directory</span><span class="sxs-lookup"><span data-stu-id="1db86-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="1db86-161">Abra Olá Ambari da interface do usuário de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1db86-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="1db86-162">Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="1db86-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="1db86-163">No menu à esquerda do hello, clique em **grupos**.</span><span class="sxs-lookup"><span data-stu-id="1db86-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="1db86-164">Você deverá ver todos os grupos de saudação sincronizados do seu cluster de HDInsight toohello do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1db86-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Grupos listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="1db86-166">Configurar permissões de exibições do Hive</span><span class="sxs-lookup"><span data-stu-id="1db86-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="1db86-167">Abra Olá Ambari da interface do usuário de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1db86-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="1db86-168">Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="1db86-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="1db86-169">No menu à esquerda do hello, clique em **exibições**.</span><span class="sxs-lookup"><span data-stu-id="1db86-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="1db86-170">Clique em **HIVE** tooshow detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="1db86-170">Click **HIVE** tooshow hello details.</span></span>

    ![Exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="1db86-172">Clique em Olá **exibição Hive** link tooconfigure Hive exibições.</span><span class="sxs-lookup"><span data-stu-id="1db86-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="1db86-173">Role para baixo toohello **permissões** seção.</span><span class="sxs-lookup"><span data-stu-id="1db86-173">Scroll down toohello **Permissions** section.</span></span>

    ![Permissões de configuração das exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="1db86-175">Clique em **adicionar usuário** ou **adicionar grupo**e, em seguida, especifique Olá usuários ou grupos podem usar exibições do Hive.</span><span class="sxs-lookup"><span data-stu-id="1db86-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="1db86-176">Configurar usuários para funções hello</span><span class="sxs-lookup"><span data-stu-id="1db86-176">Configure users for hello roles</span></span>
 <span data-ttu-id="1db86-177">toosee uma lista de funções e suas permissões, consulte [clusters HDInsight funções de domínio](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="1db86-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="1db86-178">Abra Olá Ambari da interface do usuário de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1db86-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="1db86-179">Consulte [Olá aberto da interface do usuário de gerenciamento do Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="1db86-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="1db86-180">No menu à esquerda do hello, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="1db86-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="1db86-181">Clique em **adicionar usuário** ou **adicionar grupo** tooassign usuários e grupos de funções de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="1db86-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1db86-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1db86-182">Next steps</span></span>
* <span data-ttu-id="1db86-183">Para configurar um cluster do HDInsight ingressado no domínio, confira [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurar clusters do HDInsight Ingressado no Domínio).</span><span class="sxs-lookup"><span data-stu-id="1db86-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="1db86-184">Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="1db86-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="1db86-185">Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="1db86-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
