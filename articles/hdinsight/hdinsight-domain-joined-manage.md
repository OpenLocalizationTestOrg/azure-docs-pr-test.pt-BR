---
title: "Gerenciar clusters do HDInsight ingressados no domínio – Azure | Microsoft Docs"
description: "Saiba como gerenciar clusters do HDInsight Ingressado no Domínio"
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
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="c9284-103">Gerenciar clusters do HDInsight Ingressado no Domínio (Preview)</span><span class="sxs-lookup"><span data-stu-id="c9284-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="c9284-104">Conheça os usuários e as funções do HDInsight Ingressado no Domínio e como gerenciar seus clusters.</span><span class="sxs-lookup"><span data-stu-id="c9284-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="c9284-105">Usuários dos clusters do HDInsight Ingressado no Domínio</span><span class="sxs-lookup"><span data-stu-id="c9284-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="c9284-106">Um cluster do HDInsight que não for ingressado no domínio terá duas contas de usuário que serão criadas durante a elaboração do cluster:</span><span class="sxs-lookup"><span data-stu-id="c9284-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="c9284-107">**Administração do Ambari**: essa conta também é conhecida como *usuário do Hadoop* ou *usuário HTTP*.</span><span class="sxs-lookup"><span data-stu-id="c9284-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="c9284-108">Essa conta pode ser usada para fazer logon no Ambari em https://&lt;clustername>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c9284-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="c9284-109">Ela também pode ser usada para executar consultas nas exibições do Ambari, para executar trabalhos por meio de ferramentas externas (ou seja, PowerShell, Templeton, Visual Studio) e para autenticar com o driver ODBC do Hive e com ferramentas de BI (por exemplo, Excel, PowerBI ou Tableau).</span><span class="sxs-lookup"><span data-stu-id="c9284-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="c9284-110">**Usuário do SSH**: essa conta pode ser usada com o SSH e executar comandos sudo.</span><span class="sxs-lookup"><span data-stu-id="c9284-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="c9284-111">Ela tem privilégios raiz sobre as VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c9284-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="c9284-112">Um cluster do HDInsight ingressado no domínio tem três novos usuários, além da Administração do Ambari e do Usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="c9284-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="c9284-113">**Administração do Ranger**: essa é a conta de administrador local do Apache Ranger.</span><span class="sxs-lookup"><span data-stu-id="c9284-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="c9284-114">Ela não é um usuário do Domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9284-114">It is not an active directory domain user.</span></span> <span data-ttu-id="c9284-115">Essa conta pode ser usada para configurar políticas e tornar outros usuários administradores ou administradores delegados (de modo que os usuários possam gerenciar políticas).</span><span class="sxs-lookup"><span data-stu-id="c9284-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="c9284-116">Por padrão, o nome de usuário é *administrador* e a senha é a mesma que a senha de administrador do Ambari.</span><span class="sxs-lookup"><span data-stu-id="c9284-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="c9284-117">A senha pode ser atualizada da página Configurações no Ranger.</span><span class="sxs-lookup"><span data-stu-id="c9284-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="c9284-118">**Usuário de domínio do administrador do cluster**: essa conta é um usuário do Domínio do Active Directory designado como o administrador do cluster do Hadoop, incluindo o Ambari e o Ranger.</span><span class="sxs-lookup"><span data-stu-id="c9284-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="c9284-119">Você deve fornecer as credenciais do usuário durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="c9284-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="c9284-120">Esse usuário tem os seguintes privilégios:</span><span class="sxs-lookup"><span data-stu-id="c9284-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="c9284-121">Adicionar computadores ao domínio e colocá-los na UO que você especificar durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="c9284-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="c9284-122">Criar entidades de serviço na UO que você especificar durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="c9284-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="c9284-123">Criar entradas de DNS reverso.</span><span class="sxs-lookup"><span data-stu-id="c9284-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="c9284-124">Observe que os usuários do AD também têm esses privilégios.</span><span class="sxs-lookup"><span data-stu-id="c9284-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="c9284-125">Há alguns pontos de extremidade do cluster (por exemplo, Templeton) que não são gerenciados pelo Ranger e, portanto, não são seguros.</span><span class="sxs-lookup"><span data-stu-id="c9284-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="c9284-126">Esses pontos de extremidade estão bloqueados para todos os usuários, exceto para o usuário de domínio do administrador do cluster.</span><span class="sxs-lookup"><span data-stu-id="c9284-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="c9284-127">**Regular**: durante a criação do cluster, você poderá fornecer vários grupos do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9284-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="c9284-128">Os usuários nesses grupos serão sincronizados ao Ranger e ao Ambari.</span><span class="sxs-lookup"><span data-stu-id="c9284-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="c9284-129">Esses usuários são usuários de domínio e eles terão acesso apenas aos pontos de extremidade gerenciados pelo Ranger (por exemplo, Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="c9284-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="c9284-130">Todas as políticas de RBAC e a auditoria serão aplicáveis a esses usuários.</span><span class="sxs-lookup"><span data-stu-id="c9284-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="c9284-131">Funções dos clusters do HDInsight Ingressado no Domínio</span><span class="sxs-lookup"><span data-stu-id="c9284-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="c9284-132">O HDInsight Ingressado no Domínio tem as seguintes funções:</span><span class="sxs-lookup"><span data-stu-id="c9284-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="c9284-133">Administrador do cluster</span><span class="sxs-lookup"><span data-stu-id="c9284-133">Cluster Administrator</span></span>
* <span data-ttu-id="c9284-134">Operador do cluster</span><span class="sxs-lookup"><span data-stu-id="c9284-134">Cluster Operator</span></span>
* <span data-ttu-id="c9284-135">Administrador de serviços</span><span class="sxs-lookup"><span data-stu-id="c9284-135">Service Administrator</span></span>
* <span data-ttu-id="c9284-136">Operador de serviço</span><span class="sxs-lookup"><span data-stu-id="c9284-136">Service Operator</span></span>
* <span data-ttu-id="c9284-137">Usuário do cluster</span><span class="sxs-lookup"><span data-stu-id="c9284-137">Cluster User</span></span>

<span data-ttu-id="c9284-138">**Para ver as permissões dessas funções**</span><span class="sxs-lookup"><span data-stu-id="c9284-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="c9284-139">Abra a interface do usuário do Ambari Management.</span><span class="sxs-lookup"><span data-stu-id="c9284-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c9284-140">Confira [Open the Ambari Management UI](#open-the-ambari-management-ui) (Abrir a interface do usuário do Ambari Management).</span><span class="sxs-lookup"><span data-stu-id="c9284-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c9284-141">No menu à esquerda, clique em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="c9284-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="c9284-142">Clique no ponto de interrogação azul para ver as permissões:</span><span class="sxs-lookup"><span data-stu-id="c9284-142">Click the blue question mark to see the permissions:</span></span>

    ![Permissões das funções do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="c9284-144">Abra a interface do usuário do Ambari Management</span><span class="sxs-lookup"><span data-stu-id="c9284-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="c9284-145">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9284-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c9284-146">Abra seu cluster do HDInsight em uma folha.</span><span class="sxs-lookup"><span data-stu-id="c9284-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="c9284-147">Confira [Listar e mostrar clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="c9284-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="c9284-148">Clique em **Painel** no menu superior para abrir o Ambari.</span><span class="sxs-lookup"><span data-stu-id="c9284-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="c9284-149">Faça logon no Ambari usando o nome de usuário e a senha de domínio de administrador do cluster.</span><span class="sxs-lookup"><span data-stu-id="c9284-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="c9284-150">Clique no menu suspenso **Administrador** no canto superior direito e, em seguida, clique em **Gerenciar o Ambari**.</span><span class="sxs-lookup"><span data-stu-id="c9284-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![Ambari gerenciado pelo HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="c9284-152">A interface do usuário é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="c9284-152">The UI looks like:</span></span>

    ![Interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="c9284-154">Listar os usuários de domínio sincronizados do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9284-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="c9284-155">Abra a interface do usuário do Ambari Management.</span><span class="sxs-lookup"><span data-stu-id="c9284-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c9284-156">Confira [Open the Ambari Management UI](#open-the-ambari-management-ui) (Abrir a interface do usuário do Ambari Management).</span><span class="sxs-lookup"><span data-stu-id="c9284-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c9284-157">No menu à esquerda, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c9284-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="c9284-158">Você deverá ver todos os usuários sincronizados do seu Active Directory com o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9284-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Usuários listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="c9284-160">Listar os grupos de domínio sincronizados do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9284-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="c9284-161">Abra a interface do usuário do Ambari Management.</span><span class="sxs-lookup"><span data-stu-id="c9284-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c9284-162">Confira [Open the Ambari Management UI](#open-the-ambari-management-ui) (Abrir a interface do usuário do Ambari Management).</span><span class="sxs-lookup"><span data-stu-id="c9284-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c9284-163">No menu à esquerda, clique em **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9284-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="c9284-164">Você deverá ver todos os grupos sincronizados do seu Active Directory no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9284-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Grupos listados na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="c9284-166">Configurar permissões de exibições do Hive</span><span class="sxs-lookup"><span data-stu-id="c9284-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="c9284-167">Abra a interface do usuário do Ambari Management.</span><span class="sxs-lookup"><span data-stu-id="c9284-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c9284-168">Confira [Open the Ambari Management UI](#open-the-ambari-management-ui) (Abrir a interface do usuário do Ambari Management).</span><span class="sxs-lookup"><span data-stu-id="c9284-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c9284-169">No menu à esquerda, clique em **Exibições**.</span><span class="sxs-lookup"><span data-stu-id="c9284-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="c9284-170">Clique em **HIVE** para mostrar os detalhes.</span><span class="sxs-lookup"><span data-stu-id="c9284-170">Click **HIVE** to show the details.</span></span>

    ![Exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="c9284-172">Clique no link **Exibição do Hive** para configurar as exibições do Hive.</span><span class="sxs-lookup"><span data-stu-id="c9284-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="c9284-173">Role para baixo até a seção **Permissões**.</span><span class="sxs-lookup"><span data-stu-id="c9284-173">Scroll down to the **Permissions** section.</span></span>

    ![Permissões de configuração das exibições do Hive na interface do usuário de gerenciamento do Ambari do HDInsight Ingressado no Domínio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="c9284-175">Clique em **Adicionar Usuário** ou **Adicionar Grupo** e, em seguida, especifique os usuários ou grupos que podem usar as exibições do Hive.</span><span class="sxs-lookup"><span data-stu-id="c9284-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="c9284-176">Configurar usuários para as funções</span><span class="sxs-lookup"><span data-stu-id="c9284-176">Configure users for the roles</span></span>
 <span data-ttu-id="c9284-177">Para ver uma lista de funções e suas permissões, confira [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters) (Funções dos clusters do HDInsight Ingressado no Domínio).</span><span class="sxs-lookup"><span data-stu-id="c9284-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="c9284-178">Abra a interface do usuário do Ambari Management.</span><span class="sxs-lookup"><span data-stu-id="c9284-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="c9284-179">Confira [Open the Ambari Management UI](#open-the-ambari-management-ui) (Abrir a interface do usuário do Ambari Management).</span><span class="sxs-lookup"><span data-stu-id="c9284-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="c9284-180">No menu à esquerda, clique em **Funções**.</span><span class="sxs-lookup"><span data-stu-id="c9284-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="c9284-181">Clique em **Adicionar Usuário** ou **Adicionar Grupo** para atribuir usuários e grupos a funções diferentes.</span><span class="sxs-lookup"><span data-stu-id="c9284-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9284-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9284-182">Next steps</span></span>
* <span data-ttu-id="c9284-183">Para configurar um cluster do HDInsight ingressado no domínio, confira [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurar clusters do HDInsight Ingressado no Domínio).</span><span class="sxs-lookup"><span data-stu-id="c9284-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="c9284-184">Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c9284-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="c9284-185">Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="c9284-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
