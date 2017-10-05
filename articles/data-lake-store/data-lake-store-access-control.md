---
title: "Visão geral do controle de acesso no Data Lake Store | Microsoft Docs"
description: Compreenda como o controle de acesso funciona no Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="7b8fd-103">Controle de acesso no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7b8fd-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="7b8fd-104">O Azure Data Lake Store implementa um modelo de controle de acesso que deriva do HDFS que, por sua vez, deriva do modelo de controle de acesso do POSIX.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="7b8fd-105">Este artigo resume as noções básicas do modelo de controle de acesso para o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="7b8fd-106">Para saber mais sobre o modelo de controle de acesso do HDFS, veja [Guia de permissões do HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="7b8fd-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="7b8fd-107">Listas de controle de acesso em arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="7b8fd-107">Access control lists on files and folders</span></span>

<span data-ttu-id="7b8fd-108">Há dois tipos de listas de controle de acesso (ACLs), **ACLs de Acesso** e **ACLs Padrão**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="7b8fd-109">**ACLs de Acesso**: controlam o acesso a um objeto.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="7b8fd-110">Os arquivos e as pastas têm ACLs de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="7b8fd-111">**ACLs Padrão**: um "modelo" de ACLs associadas a uma pasta que determinam as ACLs de Acesso para todos os itens filhos criados nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="7b8fd-112">Os Arquivos não têm ACLs Padrão.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-112">Files do not have Default ACLs.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="7b8fd-114">As ACLs de Acesso e as ACLs Padrão têm a mesma estrutura.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="7b8fd-116">Alterar a ACL Padrão em um pai não afeta o a ACL de Acesso ou a ACL Padrão de itens filhos já existentes.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="7b8fd-117">Usuários e identidades</span><span class="sxs-lookup"><span data-stu-id="7b8fd-117">Users and identities</span></span>

<span data-ttu-id="7b8fd-118">Todos os arquivos e pastas têm permissões diferentes para estas identidades:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="7b8fd-119">O usuário proprietário do arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-119">The owning user of the file</span></span>
* <span data-ttu-id="7b8fd-120">O grupo proprietário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-120">The owning group</span></span>
* <span data-ttu-id="7b8fd-121">Usuários nomeados</span><span class="sxs-lookup"><span data-stu-id="7b8fd-121">Named users</span></span>
* <span data-ttu-id="7b8fd-122">Grupos nomeados</span><span class="sxs-lookup"><span data-stu-id="7b8fd-122">Named groups</span></span>
* <span data-ttu-id="7b8fd-123">Todos os outros usuários</span><span class="sxs-lookup"><span data-stu-id="7b8fd-123">All other users</span></span>

<span data-ttu-id="7b8fd-124">As identidades dos usuários e grupos são identidades do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7b8fd-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="7b8fd-125">Portanto, a menos que indicado em contrário, um "usuário," no contexto do Data Lake Store, pode significar um usuário do Azure AD ou um grupo de segurança do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="7b8fd-126">Permissões</span><span class="sxs-lookup"><span data-stu-id="7b8fd-126">Permissions</span></span>

<span data-ttu-id="7b8fd-127">As permissões em um objeto do sistema de arquivos são **Ler**, **Gravar** e **Executar** e podem ser usadas em arquivos e em pastas como mostrado na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="7b8fd-128">Arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-128">File</span></span>     |   <span data-ttu-id="7b8fd-129">Pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="7b8fd-130">**Ler (R)**</span><span class="sxs-lookup"><span data-stu-id="7b8fd-130">**Read (R)**</span></span> | <span data-ttu-id="7b8fd-131">Pode ler o conteúdo de um arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-131">Can read the contents of a file</span></span> | <span data-ttu-id="7b8fd-132">Requer **Ler** e **Executar** para listar o conteúdo da pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="7b8fd-133">**Gravar (W)**</span><span class="sxs-lookup"><span data-stu-id="7b8fd-133">**Write (W)**</span></span> | <span data-ttu-id="7b8fd-134">Pode gravar ou anexar a um arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-134">Can write or append to a file</span></span> | <span data-ttu-id="7b8fd-135">Requer **Gravar** e **Executar** para criar itens filhos em uma pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="7b8fd-136">**Executar (X)**</span><span class="sxs-lookup"><span data-stu-id="7b8fd-136">**Execute (X)**</span></span> | <span data-ttu-id="7b8fd-137">Não significa nada no contexto do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7b8fd-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="7b8fd-138">Necessário para percorrer os itens filhos de uma pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="7b8fd-139">Formatos abreviados para permissões</span><span class="sxs-lookup"><span data-stu-id="7b8fd-139">Short forms for permissions</span></span>

<span data-ttu-id="7b8fd-140">**RWX**é usado para indicar **Ler + Gravar + Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="7b8fd-141">Existe um formato numérico mais condensado na qual **Ler = 4**, **Gravar = 2** e **Executar = 1** e sua soma representa as permissões.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="7b8fd-142">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-142">Following are some examples.</span></span>

| <span data-ttu-id="7b8fd-143">Formato numérico</span><span class="sxs-lookup"><span data-stu-id="7b8fd-143">Numeric form</span></span> | <span data-ttu-id="7b8fd-144">Formato curto</span><span class="sxs-lookup"><span data-stu-id="7b8fd-144">Short form</span></span> |      <span data-ttu-id="7b8fd-145">O que significa</span><span class="sxs-lookup"><span data-stu-id="7b8fd-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="7b8fd-146">7</span><span class="sxs-lookup"><span data-stu-id="7b8fd-146">7</span></span>            | <span data-ttu-id="7b8fd-147">RWX</span><span class="sxs-lookup"><span data-stu-id="7b8fd-147">RWX</span></span>        | <span data-ttu-id="7b8fd-148">Ler + Gravar + Executar</span><span class="sxs-lookup"><span data-stu-id="7b8fd-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="7b8fd-149">5</span><span class="sxs-lookup"><span data-stu-id="7b8fd-149">5</span></span>            | <span data-ttu-id="7b8fd-150">R-X</span><span class="sxs-lookup"><span data-stu-id="7b8fd-150">R-X</span></span>        | <span data-ttu-id="7b8fd-151">Ler + Executar</span><span class="sxs-lookup"><span data-stu-id="7b8fd-151">Read + Execute</span></span>         |
| <span data-ttu-id="7b8fd-152">4</span><span class="sxs-lookup"><span data-stu-id="7b8fd-152">4</span></span>            | <span data-ttu-id="7b8fd-153">R--</span><span class="sxs-lookup"><span data-stu-id="7b8fd-153">R--</span></span>        | <span data-ttu-id="7b8fd-154">Ler</span><span class="sxs-lookup"><span data-stu-id="7b8fd-154">Read</span></span>                   |
| <span data-ttu-id="7b8fd-155">0</span><span class="sxs-lookup"><span data-stu-id="7b8fd-155">0</span></span>            | ---        | <span data-ttu-id="7b8fd-156">Nenhuma permissão</span><span class="sxs-lookup"><span data-stu-id="7b8fd-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="7b8fd-157">Não herdam permissões</span><span class="sxs-lookup"><span data-stu-id="7b8fd-157">Permissions do not inherit</span></span>

<span data-ttu-id="7b8fd-158">No modelo de estilo POSIX usado pelo Data Lake Store, as permissões para um item são armazenadas no próprio item.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="7b8fd-159">Em outras palavras, as permissões para um item não podem ser herdadas dos itens pais.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="7b8fd-160">Cenários comuns relacionados a permissões</span><span class="sxs-lookup"><span data-stu-id="7b8fd-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="7b8fd-161">A seguir estão alguns cenários comuns para ajudá-lo a compreender quais permissões são necessárias para executar determinadas operações em uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="7b8fd-162">Permissões necessárias para ler um arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-162">Permissions needed to read a file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="7b8fd-164">Para o arquivo a ser lido, o chamador precisa de permissões **Ler**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="7b8fd-165">Para todas as pastas na estrutura de pastas que contêm o arquivo, o chamador precisa de permissões **Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="7b8fd-166">Permissões necessárias para anexar a um arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-166">Permissions needed to append to a file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="7b8fd-168">Para o arquivo ao qual será anexado, o chamador precisa de permissões **Gravar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="7b8fd-169">Para todas as pastas que contêm o arquivo, o chamador precisa de permissões **Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="7b8fd-170">Permissões necessárias para excluir um arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-170">Permissions needed to delete a file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="7b8fd-172">Para a pasta pai, o chamador precisa de permissões **Gravar + Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="7b8fd-173">Para todas as outras pastas no caminho do arquivo, o chamador precisa de permissões **Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="7b8fd-174">Permissões de gravação não são necessárias no arquivo para excluí-lo, desde que as duas condições anteriores sejam verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="7b8fd-175">Permissões necessárias para enumerar uma pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-175">Permissions needed to enumerate a folder</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="7b8fd-177">Para a pasta a ser enumerada, o chamador precisa de permissões **Ler + Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="7b8fd-178">Para todas as pastas do ancestral, o chamador precisa de permissões **Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="7b8fd-179">Exibição de permissões no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7b8fd-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="7b8fd-180">Na folha **Data Explorer** da conta do Data Lake Store, clique em **Acesso** para ver as ACLs de um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="7b8fd-181">Clique em **Acesso** para ver as ACLs para a pasta **catálogo** sob a conta **mydatastore**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="7b8fd-183">Nessa folha, a seção superior mostra uma visão geral das permissões que você tem.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="7b8fd-184">(Na captura de tela, o usuário é Paulo.) A seguir, as permissões de acesso são mostradas.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="7b8fd-185">Depois disso, da folha **Acesso**, clique em **Exibição Simples** para ver a exibição mais simples.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="7b8fd-187">Clique em **Exibição Avançada** para ver a exibição mais avançada em que os conceitos de ACLs Padrão, máscara e superusuário são mostrados.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="7b8fd-189">O superusuário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-189">The super-user</span></span>

<span data-ttu-id="7b8fd-190">Um superusuário é aquele que tem mais direitos no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="7b8fd-191">Um superusuário:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-191">A super-user:</span></span>

* <span data-ttu-id="7b8fd-192">Tem Permissões RWX para **todos** os arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="7b8fd-193">Pode alterar as permissões em qualquer arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="7b8fd-194">Pode alterar o usuário proprietário ou o grupo proprietário de qualquer arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="7b8fd-195">No Azure, uma conta do Data Lake Store tem diversas funções do Azure, incluindo:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="7b8fd-196">Proprietários</span><span class="sxs-lookup"><span data-stu-id="7b8fd-196">Owners</span></span>
* <span data-ttu-id="7b8fd-197">Colaboradores</span><span class="sxs-lookup"><span data-stu-id="7b8fd-197">Contributors</span></span>
* <span data-ttu-id="7b8fd-198">Leitores</span><span class="sxs-lookup"><span data-stu-id="7b8fd-198">Readers</span></span>

<span data-ttu-id="7b8fd-199">Todos na função **Proprietários** para uma conta do Data Lake Store se tornam automaticamente superusuários para essa conta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="7b8fd-200">Para saber mais, confira [Controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7b8fd-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="7b8fd-201">Se você quiser criar uma função personalizada de RBAC (controle de acesso baseado em função) com permissões de superusuário, ela precisará ter as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="7b8fd-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="7b8fd-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="7b8fd-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="7b8fd-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="7b8fd-204">O usuário proprietário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-204">The owning user</span></span>

<span data-ttu-id="7b8fd-205">O usuário que criou o item é automaticamente o usuário proprietário do item.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="7b8fd-206">Um usuário proprietário pode:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-206">An owning user can:</span></span>

* <span data-ttu-id="7b8fd-207">Altere as permissões de um arquivo pertencente.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="7b8fd-208">Alterar o grupo proprietário de um arquivo pertencente, contanto que o usuário proprietário também seja membro do grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="7b8fd-209">O usuário proprietário *não pode* alterar o usuário proprietário de outro arquivo pertencente.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="7b8fd-210">Somente superusuários podem alterar o usuário proprietário de um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="7b8fd-211">O grupo proprietário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-211">The owning group</span></span>

<span data-ttu-id="7b8fd-212">Nas ACLs do POSIX, cada usuário está associado a um "grupo primário".</span><span class="sxs-lookup"><span data-stu-id="7b8fd-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="7b8fd-213">Por exemplo, o usuário "alice" pode pertencer ao grupo "finanças".</span><span class="sxs-lookup"><span data-stu-id="7b8fd-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="7b8fd-214">Alice pode pertencer também a vários grupos, mas um grupo será sempre designado como o grupo primário dela.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="7b8fd-215">No POSIX, quando Alice cria um arquivo, o grupo proprietário desse arquivo é definido como o grupo primário que, nesse caso, é "finanças".</span><span class="sxs-lookup"><span data-stu-id="7b8fd-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="7b8fd-216">Quando um novo item do sistema de arquivos é criado, o Data Lake Store atribui um valor para o grupo proprietário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="7b8fd-217">**Caso 1**: a pasta raiz "/".</span><span class="sxs-lookup"><span data-stu-id="7b8fd-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="7b8fd-218">Essa pasta é criada quando uma conta do Data Lake Store é criada.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="7b8fd-219">Nesse caso, o grupo proprietário é definido para o usuário que criou a conta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="7b8fd-220">**Caso 2** (todos os outros casos): quando um novo item é criado, o grupo proprietário é copiado da pasta pai.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="7b8fd-221">O grupo proprietário pode ser alterado por:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="7b8fd-222">Todos os superusuários.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-222">Any super-users.</span></span>
* <span data-ttu-id="7b8fd-223">O usuário proprietário, se o usuário proprietário também for membro do grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="7b8fd-224">Algoritmo de verificação de acesso</span><span class="sxs-lookup"><span data-stu-id="7b8fd-224">Access check algorithm</span></span>

<span data-ttu-id="7b8fd-225">A ilustração a seguir representa o algoritmo de verificação de acesso para contas do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Algoritmo de ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="7b8fd-227">A máscara e as "permissões efetivas"</span><span class="sxs-lookup"><span data-stu-id="7b8fd-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="7b8fd-228">A **máscara** é um valor RWX usado para limitar o acesso para **usuários nomeados**, o **grupo proprietário** e os **grupos nomeados** durante a execução do algoritmo de verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="7b8fd-229">Aqui estão os principais conceitos de mask.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="7b8fd-230">A máscara cria "permissões efetivas."</span><span class="sxs-lookup"><span data-stu-id="7b8fd-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="7b8fd-231">Ou seja, ele modifica as permissões no momento da verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="7b8fd-232">Mask pode ser editada diretamente pelo proprietário do arquivo e por todos os superusuários.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="7b8fd-233">A máscara pode remover permissões para criar a permissão efetiva.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="7b8fd-234">A mask *não pode* adicionar permissões à permissão efetiva.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="7b8fd-235">Vejamos alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-235">Let's look at some examples.</span></span> <span data-ttu-id="7b8fd-236">No exemplo a seguir, a máscara é definida como **RWX**, o que significa que a máscara não remove permissões.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="7b8fd-237">As permissões efetivas para o usuário nomeado, o grupo proprietário e o grupo nomeado não são alteradas durante a verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="7b8fd-239">No exemplo a seguir, a máscara é definida como **R-X**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="7b8fd-240">Isso significa que ela **desativa as permissões Gravar** para o **usuário nomeado**, o **grupo proprietário** e o **grupo nomeado** no momento da verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="7b8fd-242">Para referência, é aqui onde mask para um arquivo ou pasta aparece no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="7b8fd-244">Para uma nova conta do Data Lake Store, a mask da ACL de Acesso e a ACL Padrão da pasta raiz ("/") têm RWX como padrão.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="7b8fd-245">Permissões em novos arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="7b8fd-245">Permissions on new files and folders</span></span>

<span data-ttu-id="7b8fd-246">Quando um novo arquivo ou pasta é criado em uma pasta existente, a ACL Padrão na pasta pai determina:</span><span class="sxs-lookup"><span data-stu-id="7b8fd-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="7b8fd-247">ACL Padrão e ACL de Acesso de uma pasta filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="7b8fd-248">ACL de Acesso de um arquivo filho (os arquivos não têm uma ACL Padrão).</span><span class="sxs-lookup"><span data-stu-id="7b8fd-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="7b8fd-249">A ACL de acesso de uma pasta ou um arquivo filho</span><span class="sxs-lookup"><span data-stu-id="7b8fd-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="7b8fd-250">Quando uma pasta ou um arquivo filho é criada, a ACL Padrão do pai é copiada como a ACL de Acesso do arquivo ou da pasta filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="7b8fd-251">Além disso, se **outro** usuário tiver permissões RWX na ACL Padrão do pai, elas serão removidas da ACL de Acesso do item filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="7b8fd-253">Na maioria dos cenários, as informações anteriores são tudo o que você precisa saber sobre como a ACL de Acesso de um item filho é determinada.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="7b8fd-254">No entanto, se você estiver familiarizado com sistemas POSIX e quiser entender com detalhes como essa transformação é obtida, veja a seção [A função umask na criação da ACL de Acesso para arquivos e pastas novos](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="7b8fd-255">ACL Padrão de uma pasta filho</span><span class="sxs-lookup"><span data-stu-id="7b8fd-255">A child folder's Default ACL</span></span>

<span data-ttu-id="7b8fd-256">Quando uma pasta filho é criada em uma pasta pai, a ACL Padrão da pasta pai é copiado como está, para a ACL Padrão da pasta filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="7b8fd-258">Tópicos avançados para compreender as ACLs no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7b8fd-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="7b8fd-259">A seguir, alguns tópicos avançados para ajudar você a entender como as ACLs são determinadas para arquivos ou pastas do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="7b8fd-260">A função umask na criação da ACL de Acesso para arquivos e pastas novos</span><span class="sxs-lookup"><span data-stu-id="7b8fd-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="7b8fd-261">Em um sistema compatível com POSIX, o conceito geral é que umask é um valor de 9 bits na pasta pai usado para transformar a permissão para **usuário proprietário**, **grupo proprietário** e **outros** na ACL de Acesso de um novo arquivo ou pasta filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="7b8fd-262">Os bits de uma umask identificam quais bits devem ser desativados na ACL de Acesso do item filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="7b8fd-263">Dessa forma, é usado para impedir a propagação de permissões para o **usuário proprietário**, o **grupo proprietário** e **outros**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="7b8fd-264">Em um sistema HDFS, umask normalmente é uma opção de configuração de todo o site que é controlada pelos administradores.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="7b8fd-265">O Data Lake Store usa uma **umask de toda a conta** que não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="7b8fd-266">A tabela a seguir mostra o unmask para o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="7b8fd-267">Grupo de usuários</span><span class="sxs-lookup"><span data-stu-id="7b8fd-267">User group</span></span>  | <span data-ttu-id="7b8fd-268">Configuração</span><span class="sxs-lookup"><span data-stu-id="7b8fd-268">Setting</span></span> | <span data-ttu-id="7b8fd-269">Efeito na ACL de Acesso de um novo item filho</span><span class="sxs-lookup"><span data-stu-id="7b8fd-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="7b8fd-270">usuário proprietário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-270">Owning user</span></span> | ---     | <span data-ttu-id="7b8fd-271">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="7b8fd-271">No effect</span></span>                             |
| <span data-ttu-id="7b8fd-272">grupo proprietário</span><span class="sxs-lookup"><span data-stu-id="7b8fd-272">Owning group</span></span>| ---     | <span data-ttu-id="7b8fd-273">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="7b8fd-273">No effect</span></span>                             |
| <span data-ttu-id="7b8fd-274">outro</span><span class="sxs-lookup"><span data-stu-id="7b8fd-274">Other</span></span>       | <span data-ttu-id="7b8fd-275">RWX</span><span class="sxs-lookup"><span data-stu-id="7b8fd-275">RWX</span></span>     | <span data-ttu-id="7b8fd-276">Remover Ler + Gravar + Executar</span><span class="sxs-lookup"><span data-stu-id="7b8fd-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="7b8fd-277">A ilustração a seguir mostra esta umask em ação.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="7b8fd-278">O efeito líquido é remover **Ler + Gravar + Executar** para **outro** usuário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="7b8fd-279">Como a umask não especificou bits para o **usuário proprietário** e o **grupo proprietário**, essas permissões não são transformadas.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="7b8fd-281">O sticky bit</span><span class="sxs-lookup"><span data-stu-id="7b8fd-281">The sticky bit</span></span>

<span data-ttu-id="7b8fd-282">O sticky bit é um recurso mais avançado de um sistema de arquivos POSIX.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="7b8fd-283">No contexto do Data Lake Store, é improvável que o sticky bit seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="7b8fd-284">A tabela a seguir mostra como o bit adesivo funciona no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="7b8fd-285">Grupo de usuários</span><span class="sxs-lookup"><span data-stu-id="7b8fd-285">User group</span></span>         | <span data-ttu-id="7b8fd-286">Arquivo</span><span class="sxs-lookup"><span data-stu-id="7b8fd-286">File</span></span>    | <span data-ttu-id="7b8fd-287">Pasta</span><span class="sxs-lookup"><span data-stu-id="7b8fd-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="7b8fd-288">Sticky bit **DESATIVADO**</span><span class="sxs-lookup"><span data-stu-id="7b8fd-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="7b8fd-289">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="7b8fd-289">No effect</span></span>   | <span data-ttu-id="7b8fd-290">Sem efeito.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-290">No effect.</span></span>           |
| <span data-ttu-id="7b8fd-291">Sticky bit **ATIVADO**</span><span class="sxs-lookup"><span data-stu-id="7b8fd-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="7b8fd-292">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="7b8fd-292">No effect</span></span>   | <span data-ttu-id="7b8fd-293">Impede que alguém, exceto os **superusuários** e o **usuário proprietário** de um item filho, exclua ou renomeie o item filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="7b8fd-294">O sticky bit não é mostrado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="7b8fd-295">Perguntas comuns sobre ACLs no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7b8fd-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="7b8fd-296">Aqui estão algumas perguntas que surgem com frequência sobre ACLs no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="7b8fd-297">É necessário habilitar o suporte para ACLs?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="7b8fd-298">Não.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-298">No.</span></span> <span data-ttu-id="7b8fd-299">O controle de acesso via ACLs está sempre ativado para uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="7b8fd-300">Quais são as permissões necessárias para excluir recursivamente uma pasta e seu conteúdo?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="7b8fd-301">A pasta pai deve ter permissões **Gravar + Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="7b8fd-302">A pasta a ser excluída, e todas as pastas nela, exige permissões **Ler + Gravar + Executar**.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="7b8fd-303">Você não precisa de permissões de gravação para excluir arquivos em pastas.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="7b8fd-304">Além disso, a pasta raiz "/" **nunca** poderá ser excluída.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="7b8fd-305">Quem é o proprietário de um arquivo ou pasta?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="7b8fd-306">O criador de um arquivo ou pasta se torna o proprietário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="7b8fd-307">Qual grupo é definido como o grupo proprietário de um arquivo ou pasta na criação?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="7b8fd-308">O grupo pertencente é copiado do grupo proprietário da pasta pai na qual o novo arquivo ou pasta é criado.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="7b8fd-309">Eu sou o usuário proprietário de um arquivo, mas não tenho as permissões RWX de que necessito.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="7b8fd-310">O que devo fazer?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-310">What do I do?</span></span>

<span data-ttu-id="7b8fd-311">O usuário proprietário pode alterar as permissões do arquivo para atribuir a sim mesmo quaisquer permissões RWX necessárias.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="7b8fd-312">Quando examino as ACLs no portal do Azure eu vejo nomes de usuário, mas por meio de APIs eu vejo GUIDs, por quê?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="7b8fd-313">As entradas nas ACLs são armazenadas como GUIDs que correspondem aos usuários no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="7b8fd-314">As APIs retornam os GUIDs como estão.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="7b8fd-315">O portal do Azure tenta tornar as ACLs mais fáceis de usar, convertendo os GUIDs em nomes amigáveis quando possível.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="7b8fd-316">Por que, às vezes, vejo GUIDs nas ACLs ao usar o portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="7b8fd-317">Um GUID é mostrado quando o usuário não existe mais no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="7b8fd-318">Geralmente isso acontece se o usuário tiver deixado a empresa ou se sua conta tiver sido excluída no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="7b8fd-319">O Data Lake Store dá suporte à herança de ACLs?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="7b8fd-320">Não.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="7b8fd-321">Qual é a diferença entre mask e umask?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="7b8fd-322">mask</span><span class="sxs-lookup"><span data-stu-id="7b8fd-322">mask</span></span> | <span data-ttu-id="7b8fd-323">umask</span><span class="sxs-lookup"><span data-stu-id="7b8fd-323">umask</span></span>|
|------|------|
| <span data-ttu-id="7b8fd-324">A propriedade **mask** está disponível em todos os arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="7b8fd-325">**umask** é uma propriedade da conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="7b8fd-326">Portanto, há apenas uma única umask no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="7b8fd-327">A propriedade mask em um arquivo ou pasta pode ser alterada pelo usuário proprietário ou pelo grupo proprietário de um arquivo ou por um superusuário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="7b8fd-328">A propriedade umask não pode ser modificada por qualquer usuário, até mesmo por um superusuário.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="7b8fd-329">É um valor constante, inalterável.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="7b8fd-330">A propriedade mask é usada durante o algoritmo de verificação de acesso em tempo de execução para determinar se um usuário tem o direito de executar a operação em um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="7b8fd-331">A função de mask é criar "permissões efetivas" no momento da verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="7b8fd-332">A umask nunca é usada durante a verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="7b8fd-333">A umask é usada para determinar o a ACL de Acesso de novos itens filho de uma pasta.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="7b8fd-334">Mask é um valor RWX de 3 bits que se aplica ao usuário nomeado, ao grupo nomeado e ao usuário proprietário no momento da verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="7b8fd-335">Umask é um valor de 9 bits que se aplica ao usuário proprietário, ao grupo proprietário e **outros** de um novo filho.</span><span class="sxs-lookup"><span data-stu-id="7b8fd-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="7b8fd-336">Onde posso saber mais sobre o modelo de controle de acesso do POSIX?</span><span class="sxs-lookup"><span data-stu-id="7b8fd-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="7b8fd-337">Listas de controle de acesso POSIX no Linux</span><span class="sxs-lookup"><span data-stu-id="7b8fd-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="7b8fd-338">Guia de permissão do HDFS</span><span class="sxs-lookup"><span data-stu-id="7b8fd-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="7b8fd-339">PERGUNTAS FREQUENTES SOBRE O POSIX</span><span class="sxs-lookup"><span data-stu-id="7b8fd-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="7b8fd-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="7b8fd-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="7b8fd-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="7b8fd-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="7b8fd-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="7b8fd-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="7b8fd-343">POSIX ACL no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7b8fd-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="7b8fd-344">ACL usando listas de controle de acesso no Linux</span><span class="sxs-lookup"><span data-stu-id="7b8fd-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="7b8fd-345">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7b8fd-345">See also</span></span>

* [<span data-ttu-id="7b8fd-346">Visão geral do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="7b8fd-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
