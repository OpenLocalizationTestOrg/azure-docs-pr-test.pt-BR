---
title: "aaaOverview de controle de acesso no repositório Data Lake | Microsoft Docs"
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
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="3db5b-103">Controle de acesso no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3db5b-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="3db5b-104">Repositório Azure Data Lake implementa um modelo de controle de acesso que deriva de HDFS, que por sua vez deriva de modelo de controle de acesso do hello POSIX.</span><span class="sxs-lookup"><span data-stu-id="3db5b-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="3db5b-105">Este artigo resume Noções básicas de saudação do modelo de controle de acesso de saudação para repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="3db5b-106">toolearn mais sobre o modelo de controle de acesso HDFS hello, consulte [HDFS permissões guia](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="3db5b-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="3db5b-107">Listas de controle de acesso em arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="3db5b-107">Access control lists on files and folders</span></span>

<span data-ttu-id="3db5b-108">Há dois tipos de listas de controle de acesso (ACLs), **ACLs de Acesso** e **ACLs Padrão**.</span><span class="sxs-lookup"><span data-stu-id="3db5b-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="3db5b-109">**Acessar ACLs**: estes objetos de tooan de acesso de controle.</span><span class="sxs-lookup"><span data-stu-id="3db5b-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="3db5b-110">Os arquivos e as pastas têm ACLs de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3db5b-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="3db5b-111">**Padrão de ACLs**: um "modelo" de ACLs associado com uma pasta que determinam a saudação ACLs de acesso para todos os itens filho que são criados nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="3db5b-112">Os Arquivos não têm ACLs Padrão.</span><span class="sxs-lookup"><span data-stu-id="3db5b-112">Files do not have Default ACLs.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="3db5b-114">ACLs de acesso e ACLs padrão têm Olá mesma estrutura.</span><span class="sxs-lookup"><span data-stu-id="3db5b-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="3db5b-116">Olá alteração ACL padrão em um pai não afeta Olá acesso ACL ou a ACL padrão de itens filho que já existem.</span><span class="sxs-lookup"><span data-stu-id="3db5b-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="3db5b-117">Usuários e identidades</span><span class="sxs-lookup"><span data-stu-id="3db5b-117">Users and identities</span></span>

<span data-ttu-id="3db5b-118">Todos os arquivos e pastas têm permissões diferentes para estas identidades:</span><span class="sxs-lookup"><span data-stu-id="3db5b-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="3db5b-119">saudação de usuário do arquivo hello proprietário</span><span class="sxs-lookup"><span data-stu-id="3db5b-119">hello owning user of hello file</span></span>
* <span data-ttu-id="3db5b-120">grupo proprietário Olá</span><span class="sxs-lookup"><span data-stu-id="3db5b-120">hello owning group</span></span>
* <span data-ttu-id="3db5b-121">Usuários nomeados</span><span class="sxs-lookup"><span data-stu-id="3db5b-121">Named users</span></span>
* <span data-ttu-id="3db5b-122">Grupos nomeados</span><span class="sxs-lookup"><span data-stu-id="3db5b-122">Named groups</span></span>
* <span data-ttu-id="3db5b-123">Todos os outros usuários</span><span class="sxs-lookup"><span data-stu-id="3db5b-123">All other users</span></span>

<span data-ttu-id="3db5b-124">identidades de saudação de usuários e grupos são identidades do Active Directory do Azure (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3db5b-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="3db5b-125">Portanto, pode ser um "usuário," no contexto de saudação do repositório Data Lake, a menos que indicado o contrário, o significa que um usuário do AD do Azure ou um grupo de segurança do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db5b-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="3db5b-126">Permissões</span><span class="sxs-lookup"><span data-stu-id="3db5b-126">Permissions</span></span>

<span data-ttu-id="3db5b-127">Olá permissões em um objeto do sistema de arquivos são **leitura**, **gravar**, e **Execute**, e eles podem ser usados em arquivos e pastas, conforme mostrado no Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="3db5b-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="3db5b-128">Arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-128">File</span></span>     |   <span data-ttu-id="3db5b-129">Pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="3db5b-130">**Ler (R)**</span><span class="sxs-lookup"><span data-stu-id="3db5b-130">**Read (R)**</span></span> | <span data-ttu-id="3db5b-131">Pode ler o conteúdo de saudação de um arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-131">Can read hello contents of a file</span></span> | <span data-ttu-id="3db5b-132">Requer **leitura** e **Execute** conteúdo de saudação do toolist da pasta de saudação</span><span class="sxs-lookup"><span data-stu-id="3db5b-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="3db5b-133">**Gravar (W)**</span><span class="sxs-lookup"><span data-stu-id="3db5b-133">**Write (W)**</span></span> | <span data-ttu-id="3db5b-134">Pode escrever ou anexar o arquivo tooa</span><span class="sxs-lookup"><span data-stu-id="3db5b-134">Can write or append tooa file</span></span> | <span data-ttu-id="3db5b-135">Requer **gravar** e **Execute** toocreate itens de filho em uma pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="3db5b-136">**Executar (X)**</span><span class="sxs-lookup"><span data-stu-id="3db5b-136">**Execute (X)**</span></span> | <span data-ttu-id="3db5b-137">Não significa nada no contexto de saudação do repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="3db5b-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="3db5b-138">Tootraverse necessário Olá filho itens de uma pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="3db5b-139">Formatos abreviados para permissões</span><span class="sxs-lookup"><span data-stu-id="3db5b-139">Short forms for permissions</span></span>

<span data-ttu-id="3db5b-140">**RWX** é usado tooindicate **leitura + escrita + executar**.</span><span class="sxs-lookup"><span data-stu-id="3db5b-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="3db5b-141">Um formato numérico mais compacta existe no qual **leitura = 4**, **gravar = 2**, e **Execute = 1**, Olá cuja soma representa as permissões de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="3db5b-142">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="3db5b-142">Following are some examples.</span></span>

| <span data-ttu-id="3db5b-143">Formato numérico</span><span class="sxs-lookup"><span data-stu-id="3db5b-143">Numeric form</span></span> | <span data-ttu-id="3db5b-144">Formato curto</span><span class="sxs-lookup"><span data-stu-id="3db5b-144">Short form</span></span> |      <span data-ttu-id="3db5b-145">O que significa</span><span class="sxs-lookup"><span data-stu-id="3db5b-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="3db5b-146">7</span><span class="sxs-lookup"><span data-stu-id="3db5b-146">7</span></span>            | <span data-ttu-id="3db5b-147">RWX</span><span class="sxs-lookup"><span data-stu-id="3db5b-147">RWX</span></span>        | <span data-ttu-id="3db5b-148">Ler + Gravar + Executar</span><span class="sxs-lookup"><span data-stu-id="3db5b-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="3db5b-149">5</span><span class="sxs-lookup"><span data-stu-id="3db5b-149">5</span></span>            | <span data-ttu-id="3db5b-150">R-X</span><span class="sxs-lookup"><span data-stu-id="3db5b-150">R-X</span></span>        | <span data-ttu-id="3db5b-151">Ler + Executar</span><span class="sxs-lookup"><span data-stu-id="3db5b-151">Read + Execute</span></span>         |
| <span data-ttu-id="3db5b-152">4</span><span class="sxs-lookup"><span data-stu-id="3db5b-152">4</span></span>            | <span data-ttu-id="3db5b-153">R--</span><span class="sxs-lookup"><span data-stu-id="3db5b-153">R--</span></span>        | <span data-ttu-id="3db5b-154">Ler</span><span class="sxs-lookup"><span data-stu-id="3db5b-154">Read</span></span>                   |
| <span data-ttu-id="3db5b-155">0</span><span class="sxs-lookup"><span data-stu-id="3db5b-155">0</span></span>            | ---        | <span data-ttu-id="3db5b-156">Nenhuma permissão</span><span class="sxs-lookup"><span data-stu-id="3db5b-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="3db5b-157">Não herdam permissões</span><span class="sxs-lookup"><span data-stu-id="3db5b-157">Permissions do not inherit</span></span>

<span data-ttu-id="3db5b-158">No modelo de estilo POSIX Olá que é usado pelo repositório Data Lake, permissões para um item são armazenadas no próprio item hello.</span><span class="sxs-lookup"><span data-stu-id="3db5b-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="3db5b-159">Em outras palavras, as permissões para um item não podem ser herdadas Olá itens de pai.</span><span class="sxs-lookup"><span data-stu-id="3db5b-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="3db5b-160">Toopermissions relacionados de cenários comuns</span><span class="sxs-lookup"><span data-stu-id="3db5b-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="3db5b-161">Estes são alguns toohelp cenários comuns entender quais permissões são necessárias tooperform determinadas operações em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="3db5b-162">Permissões necessárias tooread um arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-162">Permissions needed tooread a file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="3db5b-164">Para toobe de arquivo hello ler, Olá chamador necessidades **leitura** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="3db5b-165">Para todos os hello pastas na estrutura de pastas de saudação que contêm o arquivo hello, Olá chamador necessidades **Execute** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="3db5b-166">Permissões necessárias tooappend tooa arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-166">Permissions needed tooappend tooa file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="3db5b-168">Para toobe do arquivo hello anexados ao, Olá chamador necessidades **gravar** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="3db5b-169">Para todos os hello pastas que contêm o arquivo hello, Olá chamador necessidades **Execute** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="3db5b-170">Permissões necessárias toodelete um arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-170">Permissions needed toodelete a file</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="3db5b-172">Para a pasta pai Olá Olá chamador necessidades **gravar + executar** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="3db5b-173">Para todos os hello outras pastas no caminho do arquivo hello, Olá chamador necessidades **Execute** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="3db5b-174">Grave as permissões no arquivo hello não são necessária toodelete-desde Olá anteriores duas condições forem verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="3db5b-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="3db5b-175">Permissões necessárias tooenumerate uma pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-175">Permissions needed tooenumerate a folder</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="3db5b-177">Para Olá pasta tooenumerate, Olá chamador necessidades **leitura + Execute** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="3db5b-178">Para todos os hello pastas ancestral, Olá chamador necessidades **Execute** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="3db5b-179">Exibindo permissões no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3db5b-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="3db5b-180">De saudação **Data Explorer** folha de saudação conta do repositório Data Lake, clique em **acesso** toosee Olá ACLs para um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="3db5b-181">Clique em **acesso** toosee Olá ACLs para Olá **catálogo** pasta sob Olá **mydatastore** conta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="3db5b-183">Esta folha, seção superior Olá mostra uma visão geral das permissões de saudação que você possui.</span><span class="sxs-lookup"><span data-stu-id="3db5b-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="3db5b-184">(Na captura de tela hello, o usuário Olá é Bob.) Depois disso, as permissões de acesso de saudação são mostradas.</span><span class="sxs-lookup"><span data-stu-id="3db5b-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="3db5b-185">Depois disso, da saudação **acesso** folha, clique em **exibição simples** toosee Olá exibição simples.</span><span class="sxs-lookup"><span data-stu-id="3db5b-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="3db5b-187">Clique em **exibição avançada** toosee hello mais exibição avançada, onde os conceitos de saudação de ACLs padrão, a máscara e o superusuário são mostrados.</span><span class="sxs-lookup"><span data-stu-id="3db5b-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="3db5b-189">superusuário Olá</span><span class="sxs-lookup"><span data-stu-id="3db5b-189">hello super-user</span></span>

<span data-ttu-id="3db5b-190">Um superusuário tem Olá a maioria dos direitos de todos os usuários Olá Olá repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="3db5b-191">Um superusuário:</span><span class="sxs-lookup"><span data-stu-id="3db5b-191">A super-user:</span></span>

* <span data-ttu-id="3db5b-192">Tem permissões de RWX muito**todos os** arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="3db5b-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="3db5b-193">Pode alterar permissões hello em qualquer arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="3db5b-194">Pode alterar Olá possui um usuário ou grupo de qualquer arquivo ou pasta proprietário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="3db5b-195">No Azure, uma conta do Data Lake Store tem diversas funções do Azure, incluindo:</span><span class="sxs-lookup"><span data-stu-id="3db5b-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="3db5b-196">Proprietários</span><span class="sxs-lookup"><span data-stu-id="3db5b-196">Owners</span></span>
* <span data-ttu-id="3db5b-197">Colaboradores</span><span class="sxs-lookup"><span data-stu-id="3db5b-197">Contributors</span></span>
* <span data-ttu-id="3db5b-198">Leitores</span><span class="sxs-lookup"><span data-stu-id="3db5b-198">Readers</span></span>

<span data-ttu-id="3db5b-199">Todos no hello **proprietários** função para uma conta do repositório Data Lake é automaticamente um superusuário para essa conta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="3db5b-200">mais, consulte toolearn [controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3db5b-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="3db5b-201">Se você quiser toocreate uma função de controle de acesso baseado em função (RBAC) personalizado que tenha permissões de superusuário, ele precisa Olá toohave as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="3db5b-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="3db5b-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="3db5b-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="3db5b-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="3db5b-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="3db5b-204">usuário proprietário Olá</span><span class="sxs-lookup"><span data-stu-id="3db5b-204">hello owning user</span></span>

<span data-ttu-id="3db5b-205">usuário Olá que criou o item de saudação é automaticamente Olá usuário do item de saudação de proprietário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="3db5b-206">Um usuário proprietário pode:</span><span class="sxs-lookup"><span data-stu-id="3db5b-206">An owning user can:</span></span>

* <span data-ttu-id="3db5b-207">Alterar permissões de saudação de um arquivo que é de propriedade.</span><span class="sxs-lookup"><span data-stu-id="3db5b-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="3db5b-208">Alterar Olá possui o grupo de um arquivo que é de propriedade, como usuário proprietário Olá também é um membro do grupo de destino hello.</span><span class="sxs-lookup"><span data-stu-id="3db5b-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="3db5b-209">Olá usuário proprietário *não é possível* alterar Olá possui um usuário de outro arquivo de propriedade.</span><span class="sxs-lookup"><span data-stu-id="3db5b-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="3db5b-210">Somente super usuários podem alterar Olá possui um usuário de um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="3db5b-211">grupo proprietário Olá</span><span class="sxs-lookup"><span data-stu-id="3db5b-211">hello owning group</span></span>

<span data-ttu-id="3db5b-212">Olá POSIX ACLs, cada usuário é associado um "grupo primário".</span><span class="sxs-lookup"><span data-stu-id="3db5b-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="3db5b-213">Por exemplo, o usuário "alice" pode pertencer toohello grupo de "financeiro".</span><span class="sxs-lookup"><span data-stu-id="3db5b-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="3db5b-214">Alice também pode pertencer a grupos de toomultiple, mas um grupo sempre é designado como o grupo primário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="3db5b-215">POSIX, quando Alice cria um arquivo, Olá possui o grupo de arquivo é definido grupo primário tooher, que nesse caso é "Finanças".</span><span class="sxs-lookup"><span data-stu-id="3db5b-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="3db5b-216">Quando um novo item do sistema de arquivos é criado, o repositório Data Lake atribui toohello um valor que possui o grupo.</span><span class="sxs-lookup"><span data-stu-id="3db5b-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="3db5b-217">**Caso 1**: pasta raiz de hello "/".</span><span class="sxs-lookup"><span data-stu-id="3db5b-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="3db5b-218">Essa pasta é criada quando uma conta do Data Lake Store é criada.</span><span class="sxs-lookup"><span data-stu-id="3db5b-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="3db5b-219">Nesse caso, o grupo proprietário Olá é definido usuário toohello que criou a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="3db5b-220">**Caso 2** (qualquer outro caso): quando um novo item é criado, grupo proprietário Olá é copiado da pasta pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="3db5b-221">grupo proprietário Olá pode ser alterado por:</span><span class="sxs-lookup"><span data-stu-id="3db5b-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="3db5b-222">Todos os superusuários.</span><span class="sxs-lookup"><span data-stu-id="3db5b-222">Any super-users.</span></span>
* <span data-ttu-id="3db5b-223">saudação do usuário, proprietário, se o usuário proprietário Olá também é um membro do grupo de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="3db5b-224">Algoritmo de verificação de acesso</span><span class="sxs-lookup"><span data-stu-id="3db5b-224">Access check algorithm</span></span>

<span data-ttu-id="3db5b-225">Olá ilustração a seguir representa o algoritmo de verificação de acesso Olá para contas do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algoritmo de ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="3db5b-227">Olá e máscara "permissões efetivas"</span><span class="sxs-lookup"><span data-stu-id="3db5b-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="3db5b-228">Olá **máscara** é um RWX valor que é usado toolimit acesso **usuários nomeados**, Olá **grupo proprietário**, e **grupos nomeados** quando estiver algoritmo de verificação de acesso de execução hello.</span><span class="sxs-lookup"><span data-stu-id="3db5b-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="3db5b-229">Aqui estão os principais conceitos Olá para máscara hello.</span><span class="sxs-lookup"><span data-stu-id="3db5b-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="3db5b-230">máscara de saudação cria "permissões efetivas".</span><span class="sxs-lookup"><span data-stu-id="3db5b-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="3db5b-231">Ou seja, modifica as permissões de saudação em tempo de saudação de verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="3db5b-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="3db5b-232">máscara de saudação pode ser editada diretamente pelo proprietário do arquivo hello e quaisquer super usuários.</span><span class="sxs-lookup"><span data-stu-id="3db5b-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="3db5b-233">máscara de saudação pode remover a permissão efetiva do permissões toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="3db5b-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="3db5b-234">máscara de saudação *não é possível* adicionar permissão efetiva do toohello de permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="3db5b-235">Vejamos alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="3db5b-235">Let's look at some examples.</span></span> <span data-ttu-id="3db5b-236">Saudação de exemplo a seguir, máscara de saudação é definida muito**RWX**, que significa que essa máscara Olá não remova as permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="3db5b-237">permissões efetivas Olá Olá usuário, grupo de proprietário e denominado grupo nomeado não são alteradas durante a verificação de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="3db5b-239">Saudação de exemplo a seguir, máscara de saudação é definida muito**R-X**.</span><span class="sxs-lookup"><span data-stu-id="3db5b-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="3db5b-240">Isso significa que ele **desativa permissões de gravação da saudação** para **usuário nomeado**, **grupo proprietário**, e **denominado grupo** em tempo de saudação do access seleção.</span><span class="sxs-lookup"><span data-stu-id="3db5b-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="3db5b-242">Para referência, aqui é onde a máscara de saudação para um arquivo ou pasta aparece na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db5b-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="3db5b-244">Para obter uma nova conta do repositório Data Lake, máscara Olá Olá acesso ACL e ACL padrão da raiz de saudação ("/") de pasta padrão é tooRWX.</span><span class="sxs-lookup"><span data-stu-id="3db5b-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="3db5b-245">Permissões em novos arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="3db5b-245">Permissions on new files and folders</span></span>

<span data-ttu-id="3db5b-246">Quando um novo arquivo ou pasta é criada em uma pasta existente, a saudação padrão ACL na pasta pai de saudação determina:</span><span class="sxs-lookup"><span data-stu-id="3db5b-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="3db5b-247">ACL Padrão e ACL de Acesso de uma pasta filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="3db5b-248">ACL de Acesso de um arquivo filho (os arquivos não têm uma ACL Padrão).</span><span class="sxs-lookup"><span data-stu-id="3db5b-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="3db5b-249">Olá acesso ACL de um filho de arquivo ou pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="3db5b-250">Quando um arquivo filho ou uma pasta é criada, padrão ACL do pai da saudação é copiada como Olá Olá filho arquivo ou pasta de acesso ACL.</span><span class="sxs-lookup"><span data-stu-id="3db5b-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="3db5b-251">Além disso, se **outros** usuário tem permissões de RWX na ACL padrão de saudação pai, ele será removido da ACL de acesso do item do hello filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="3db5b-253">Na maioria dos cenários, as informações anteriores Olá são que tudo o que você precisa tooknow sobre como acesso ACL de um item filho é determinada.</span><span class="sxs-lookup"><span data-stu-id="3db5b-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="3db5b-254">No entanto, se você estiver familiarizado com os sistemas POSIX e quiser toounderstand detalhada como essa transformação é obtida, consulte a seção Olá [função do Umask na criação de saudação acesso ACL para novos arquivos e pastas](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3db5b-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="3db5b-255">ACL Padrão de uma pasta filho</span><span class="sxs-lookup"><span data-stu-id="3db5b-255">A child folder's Default ACL</span></span>

<span data-ttu-id="3db5b-256">Quando uma pasta filho é criada em uma pasta pai, padrão ACL da pasta do pai de saudação é copiada sobre como está a ACL de padrão da pasta do toohello filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="3db5b-258">Tópicos avançados para compreender as ACLs no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3db5b-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="3db5b-259">A seguir estão alguns toohelp tópicos avançados que você entender como as ACLs são determinadas por pastas ou arquivos de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="3db5b-260">Função do umask na criação de saudação acesso ACL para novos arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="3db5b-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="3db5b-261">Em um sistema compatível com o POSIX, conceito geral Olá é que umask é um valor de 9 bits na pasta pai Olá que usou permissão Olá tootransform **usuário proprietário**, **grupo proprietário**, e  **outros** em Olá acesso ACL de um novo arquivo filho ou uma pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="3db5b-262">bits de saudação de um umask identificam quais tooturn bits desativado na ACL de acesso do item do hello filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="3db5b-263">Assim, ele é usado tooselectively impedir a propagação de saudação de permissões para **usuário proprietário**, **grupo proprietário**, e **outros**.</span><span class="sxs-lookup"><span data-stu-id="3db5b-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="3db5b-264">Em um sistema HDFS, Olá umask costuma ser uma opção de configuração de todo o site é controlada por administradores.</span><span class="sxs-lookup"><span data-stu-id="3db5b-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="3db5b-265">O Data Lake Store usa uma **umask de toda a conta** que não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="3db5b-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="3db5b-266">Olá a seguinte tabela mostra Olá sem máscara para repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="3db5b-267">Grupo de usuários</span><span class="sxs-lookup"><span data-stu-id="3db5b-267">User group</span></span>  | <span data-ttu-id="3db5b-268">Configuração</span><span class="sxs-lookup"><span data-stu-id="3db5b-268">Setting</span></span> | <span data-ttu-id="3db5b-269">Efeito na ACL de Acesso de um novo item filho</span><span class="sxs-lookup"><span data-stu-id="3db5b-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="3db5b-270">usuário proprietário</span><span class="sxs-lookup"><span data-stu-id="3db5b-270">Owning user</span></span> | ---     | <span data-ttu-id="3db5b-271">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="3db5b-271">No effect</span></span>                             |
| <span data-ttu-id="3db5b-272">grupo proprietário</span><span class="sxs-lookup"><span data-stu-id="3db5b-272">Owning group</span></span>| ---     | <span data-ttu-id="3db5b-273">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="3db5b-273">No effect</span></span>                             |
| <span data-ttu-id="3db5b-274">outro</span><span class="sxs-lookup"><span data-stu-id="3db5b-274">Other</span></span>       | <span data-ttu-id="3db5b-275">RWX</span><span class="sxs-lookup"><span data-stu-id="3db5b-275">RWX</span></span>     | <span data-ttu-id="3db5b-276">Remover Ler + Gravar + Executar</span><span class="sxs-lookup"><span data-stu-id="3db5b-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="3db5b-277">Olá ilustração a seguir mostra essa umask em ação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="3db5b-278">efeito de saudação é tooremove **leitura + escrita + executar** para **outros** usuário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="3db5b-279">Porque Olá umask não especificou o bits para **usuário proprietário** e **grupo proprietário**, essas permissões não são transformadas.</span><span class="sxs-lookup"><span data-stu-id="3db5b-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACLs do Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="3db5b-281">bit Autoadesivas Olá</span><span class="sxs-lookup"><span data-stu-id="3db5b-281">hello sticky bit</span></span>

<span data-ttu-id="3db5b-282">bit Autoadesivas Olá é um recurso mais avançado de um sistema de arquivos POSIX.</span><span class="sxs-lookup"><span data-stu-id="3db5b-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="3db5b-283">No contexto de saudação do repositório Data Lake, é improvável que esse bit Autoadesivas hello serão necessários.</span><span class="sxs-lookup"><span data-stu-id="3db5b-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="3db5b-284">Olá tabela a seguir mostra como bit Autoadesivas Olá funciona no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="3db5b-285">Grupo de usuários</span><span class="sxs-lookup"><span data-stu-id="3db5b-285">User group</span></span>         | <span data-ttu-id="3db5b-286">Arquivo</span><span class="sxs-lookup"><span data-stu-id="3db5b-286">File</span></span>    | <span data-ttu-id="3db5b-287">Pasta</span><span class="sxs-lookup"><span data-stu-id="3db5b-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="3db5b-288">Sticky bit **DESATIVADO**</span><span class="sxs-lookup"><span data-stu-id="3db5b-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="3db5b-289">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="3db5b-289">No effect</span></span>   | <span data-ttu-id="3db5b-290">Sem efeito.</span><span class="sxs-lookup"><span data-stu-id="3db5b-290">No effect.</span></span>           |
| <span data-ttu-id="3db5b-291">Sticky bit **ATIVADO**</span><span class="sxs-lookup"><span data-stu-id="3db5b-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="3db5b-292">Sem efeito</span><span class="sxs-lookup"><span data-stu-id="3db5b-292">No effect</span></span>   | <span data-ttu-id="3db5b-293">Impede que qualquer pessoa exceto **super usuários** e hello **usuário proprietário** de um item filho de excluir ou renomear o item filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="3db5b-294">bit Autoadesivas Olá não é mostrada em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db5b-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="3db5b-295">Perguntas comuns sobre ACLs no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3db5b-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="3db5b-296">Aqui estão algumas perguntas que surgem com frequência sobre ACLs no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3db5b-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="3db5b-297">É necessário o suporte para ACLs tooenable?</span><span class="sxs-lookup"><span data-stu-id="3db5b-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="3db5b-298">Não.</span><span class="sxs-lookup"><span data-stu-id="3db5b-298">No.</span></span> <span data-ttu-id="3db5b-299">O controle de acesso via ACLs está sempre ativado para uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3db5b-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="3db5b-300">Quais permissões são necessárias toorecursively excluir uma pasta e seu conteúdo?</span><span class="sxs-lookup"><span data-stu-id="3db5b-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="3db5b-301">a pasta pai Olá deve ter **gravar + executar** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="3db5b-302">Olá toobe pasta excluída e requer que todas as pastas dentro dele, **leitura + escrita + executar** permissões.</span><span class="sxs-lookup"><span data-stu-id="3db5b-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="3db5b-303">Não é necessário gravar permissões toodelete arquivos em pastas.</span><span class="sxs-lookup"><span data-stu-id="3db5b-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="3db5b-304">Além disso, Olá pasta raiz "/" pode **nunca** ser excluído.</span><span class="sxs-lookup"><span data-stu-id="3db5b-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="3db5b-305">Quem é o proprietário de saudação de um arquivo ou pasta?</span><span class="sxs-lookup"><span data-stu-id="3db5b-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="3db5b-306">Criador de saudação de um arquivo ou pasta se torna o proprietário de saudação.</span><span class="sxs-lookup"><span data-stu-id="3db5b-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="3db5b-307">Qual grupo está definido como Olá possui o grupo de um arquivo ou pasta no momento da criação?</span><span class="sxs-lookup"><span data-stu-id="3db5b-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="3db5b-308">grupo proprietário Olá é copiado da saudação possui o grupo da pasta pai de saudação sob o qual Olá novo arquivo ou pasta é criada.</span><span class="sxs-lookup"><span data-stu-id="3db5b-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="3db5b-309">Estou Olá possui um usuário de um arquivo, mas não tenho permissões de RWX Olá que necessário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="3db5b-310">O que devo fazer?</span><span class="sxs-lookup"><span data-stu-id="3db5b-310">What do I do?</span></span>

<span data-ttu-id="3db5b-311">usuário proprietário Olá pode alterar permissões Olá Olá arquivo toogive se qualquer RWX permissões precisam.</span><span class="sxs-lookup"><span data-stu-id="3db5b-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="3db5b-312">Quando vejo as ACLs no hello portal do Azure, consulte nomes de usuário, mas por meio de APIs, vejo que os GUIDs, por quê?</span><span class="sxs-lookup"><span data-stu-id="3db5b-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="3db5b-313">Entradas no hello ACLs são armazenadas como GUIDs que correspondem a toousers no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db5b-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="3db5b-314">Olá APIs retornar Olá GUIDs como está.</span><span class="sxs-lookup"><span data-stu-id="3db5b-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="3db5b-315">Olá portal do Azure tenta toomake ACLs mais fácil toouse por conversão Olá GUIDs em nomes amigáveis, quando possível.</span><span class="sxs-lookup"><span data-stu-id="3db5b-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="3db5b-316">Por que às vezes, vejo GUIDs Olá ACLs ao usar o hello portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="3db5b-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="3db5b-317">Um GUID é mostrado ao usuário Olá não existe no AD do Azure mais.</span><span class="sxs-lookup"><span data-stu-id="3db5b-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="3db5b-318">Normalmente, isso ocorre quando o usuário Olá saiu da empresa de saudação ou se sua conta foi excluída no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db5b-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="3db5b-319">O Data Lake Store dá suporte à herança de ACLs?</span><span class="sxs-lookup"><span data-stu-id="3db5b-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="3db5b-320">Não.</span><span class="sxs-lookup"><span data-stu-id="3db5b-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="3db5b-321">Qual é a diferença de saudação entre máscara e umask?</span><span class="sxs-lookup"><span data-stu-id="3db5b-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="3db5b-322">mask</span><span class="sxs-lookup"><span data-stu-id="3db5b-322">mask</span></span> | <span data-ttu-id="3db5b-323">umask</span><span class="sxs-lookup"><span data-stu-id="3db5b-323">umask</span></span>|
|------|------|
| <span data-ttu-id="3db5b-324">Olá **máscara** propriedade está disponível em cada arquivo e pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="3db5b-325">Olá **umask** é uma propriedade de saudação conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="3db5b-326">Portanto, há apenas um único umask em Olá repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3db5b-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="3db5b-327">propriedade de máscara de saudação em um arquivo ou pasta pode ser alterada por Olá possui um usuário ou grupo de um arquivo ou um superusuário proprietário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="3db5b-328">propriedade de umask Olá não pode ser modificada por qualquer usuário, até mesmo um superusuário.</span><span class="sxs-lookup"><span data-stu-id="3db5b-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="3db5b-329">É um valor constante, inalterável.</span><span class="sxs-lookup"><span data-stu-id="3db5b-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="3db5b-330">propriedade de máscara de saudação é usada durante o algoritmo de verificação de acesso de saudação em tempo de execução toodetermine se um usuário tem tooperform direita Olá em operação em um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="3db5b-331">função Hello máscara Olá é toocreate "permissões efetivas" em tempo de saudação de verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="3db5b-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="3db5b-332">Olá umask não é usado em todos os durante a verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="3db5b-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="3db5b-333">Olá umask é usado toodetermine Olá acesso ACL de novos itens filho de uma pasta.</span><span class="sxs-lookup"><span data-stu-id="3db5b-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="3db5b-334">máscara de saudação é um valor RWX de 3 bits que se aplica a toonamed usuário, grupo nomeado e usuário proprietário no tempo de saudação de verificação de acesso.</span><span class="sxs-lookup"><span data-stu-id="3db5b-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="3db5b-335">Olá, umask é um valor de 9 bits que se aplica a toohello possui um usuário, grupo, proprietário e **outros** de um novo filho.</span><span class="sxs-lookup"><span data-stu-id="3db5b-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="3db5b-336">Onde posso saber mais sobre o modelo de controle de acesso do POSIX?</span><span class="sxs-lookup"><span data-stu-id="3db5b-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="3db5b-337">Listas de controle de acesso POSIX no Linux</span><span class="sxs-lookup"><span data-stu-id="3db5b-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="3db5b-338">Guia de permissão do HDFS</span><span class="sxs-lookup"><span data-stu-id="3db5b-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="3db5b-339">PERGUNTAS FREQUENTES SOBRE O POSIX</span><span class="sxs-lookup"><span data-stu-id="3db5b-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="3db5b-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="3db5b-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="3db5b-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="3db5b-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="3db5b-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="3db5b-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="3db5b-343">POSIX ACL no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3db5b-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="3db5b-344">ACL usando listas de controle de acesso no Linux</span><span class="sxs-lookup"><span data-stu-id="3db5b-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="3db5b-345">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3db5b-345">See also</span></span>

* [<span data-ttu-id="3db5b-346">Visão geral do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="3db5b-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
