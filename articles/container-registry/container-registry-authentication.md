---
title: "aaaAuthenticate com um registro de contêiner do Azure | Microsoft Docs"
description: "Como toolog no registro do contêiner do Azure tooan usando um Active Directory do Azure do serviço principal ou uma conta de administrador"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="b8fb8-103">Autenticar com um Registro de contêiner privado do Docker</span><span class="sxs-lookup"><span data-stu-id="b8fb8-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="b8fb8-104">toowork com imagens de contêiner em um registro de contêiner do Azure, que você faça logon usando Olá `docker login` comando.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="b8fb8-105">Você pode fazer logon usando uma **[entidade de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou uma **conta de administrador** específica do registro.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="b8fb8-106">Este artigo fornece mais detalhes sobre essas identidades.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="b8fb8-107">Entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="b8fb8-107">Service principal</span></span>

<span data-ttu-id="b8fb8-108">Você pode [atribuir uma entidade de serviço](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registro e usá-lo para a autenticação básica do Docker.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="b8fb8-109">Usar uma entidade de serviço é recomendado para a maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="b8fb8-110">Fornecer ID do aplicativo hello e a senha da saudação serviço principal toohello `docker login` de comando, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b8fb8-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="b8fb8-111">Depois de conectado, Docker armazena em cache as credenciais Olá, que exige o ID do aplicativo hello. tooremember</span><span class="sxs-lookup"><span data-stu-id="b8fb8-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="b8fb8-112">Se desejar, você pode regenerar senha saudação de uma entidade de serviço executando Olá `az ad sp reset-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="b8fb8-113">Permitir que as entidades de serviço [acesso baseado em função](../active-directory/role-based-access-control-configure.md) tooa registro.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="b8fb8-114">As funções disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="b8fb8-114">Available roles are:</span></span>
  * <span data-ttu-id="b8fb8-115">Leitor (acesso somente de pull).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="b8fb8-116">Colaborador (pull e push).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="b8fb8-117">Proprietário (pull, push e atribuir funções tooother usuários).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="b8fb8-118">Acesso anônimo não está disponível em Registros de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="b8fb8-119">Para imagens públicas, você pode usar o [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="b8fb8-120">Você pode atribuir várias entidades de serviço do registro tooa, o que permite a você acesso toodefine para diferentes usuários ou aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="b8fb8-121">Entidades de serviço também habilitar registro tooa conectividade "sem cabeçalho" desenvolvedor ou cenários de DevOps como Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8fb8-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="b8fb8-122">Implantações do contêiner de sistemas de tooorchestration de registro, incluindo DC/OS, Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="b8fb8-123">Você também pode extrair contêiner registros toorelated serviços do Azure como [serviço de contêiner](../container-service/index.yml), [do serviço de aplicativo](../app-service/index.md), [lote](../batch/index.md), [Service Fabric](/azure/service-fabric/)e outros.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="b8fb8-124">Contínua integração e implantação de soluções (como o Visual Studio Team Services ou Jenkins) criar imagens de contêiner e enviá-las tooa registro.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="b8fb8-125">Conta de administrador</span><span class="sxs-lookup"><span data-stu-id="b8fb8-125">Admin account</span></span>
<span data-ttu-id="b8fb8-126">Com cada registro que você cria, uma conta de administrador é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="b8fb8-127">Por padrão a conta hello está desabilitada, mas você pode habilitá-lo e gerenciar credenciais de hello, por exemplo por meio da saudação [portal](container-registry-get-started-portal.md#manage-registry-settings) ou usando Olá [comandos do Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="b8fb8-128">Cada conta do administrador é fornecida com duas senhas, que podem ser regeneradas.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="b8fb8-129">as duas senhas de saudação permitem toomaintain do registro toohello de conexões usando uma senha enquanto você regenera Olá outra senha.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="b8fb8-130">Se Olá conta estiver habilitada, você pode passar o nome de usuário de saudação e a senha toohello `docker login` comando de registro de toohello de autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="b8fb8-131">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b8fb8-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="b8fb8-132">conta de administrador Olá destina-se um único usuário tooaccess saudação do registro, principalmente para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="b8fb8-133">Não é recomendável credenciais da conta de administrador tooshare Olá entre outros usuários.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="b8fb8-134">Todos os usuários aparecem como um registro de toohello de usuário único.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="b8fb8-135">Alterar ou desabilitar esta conta desabilita o acesso de registro para todos os usuários que usam credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="b8fb8-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="b8fb8-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8fb8-136">Next steps</span></span>
* <span data-ttu-id="b8fb8-137">[Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="b8fb8-138">Para obter mais informações sobre a autenticação na visualização de registro de contêiner hello, consulte Olá [postagem de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="b8fb8-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
