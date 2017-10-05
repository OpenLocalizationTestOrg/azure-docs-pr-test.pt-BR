---
title: "Autenticar com um registro de contêiner do Azure | Microsoft Docs"
description: "Como fazer logon em um registro de contêiner do Azure usando uma entidade de serviço do Azure Active Directory em uma conta de administrador"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="26d7e-103">Autenticar com um Registro de contêiner privado do Docker</span><span class="sxs-lookup"><span data-stu-id="26d7e-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="26d7e-104">Para trabalhar com imagens de contêiner em um registro de contêiner do Azure, você faz logon usando o comando `docker login`.</span><span class="sxs-lookup"><span data-stu-id="26d7e-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="26d7e-105">Você pode fazer logon usando uma **[entidade de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou uma **conta de administrador** específica do registro.</span><span class="sxs-lookup"><span data-stu-id="26d7e-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="26d7e-106">Este artigo fornece mais detalhes sobre essas identidades.</span><span class="sxs-lookup"><span data-stu-id="26d7e-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="26d7e-107">Entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="26d7e-107">Service principal</span></span>

<span data-ttu-id="26d7e-108">Você pode [atribuir uma entidade de serviço](container-registry-get-started-azure-cli.md#assign-a-service-principal) ao seu registro e usá-la para autenticação básica do Docker.</span><span class="sxs-lookup"><span data-stu-id="26d7e-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="26d7e-109">Usar uma entidade de serviço é recomendado para a maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="26d7e-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="26d7e-110">Forneça a ID do aplicativo e a senha da entidade de serviço para o comando `docker login`, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="26d7e-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="26d7e-111">Depois de conectado, o Docker armazena em cache as credenciais, portanto, você não precisa se lembrar da ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26d7e-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="26d7e-112">Se quiser, você pode regenerar a senha de uma entidade de serviço executando o comando `az ad sp reset-credentials`.</span><span class="sxs-lookup"><span data-stu-id="26d7e-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="26d7e-113">As entidades de serviço permitem o [acesso baseado em função](../active-directory/role-based-access-control-configure.md) a um registro.</span><span class="sxs-lookup"><span data-stu-id="26d7e-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="26d7e-114">As funções disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="26d7e-114">Available roles are:</span></span>
  * <span data-ttu-id="26d7e-115">Leitor (acesso somente de pull).</span><span class="sxs-lookup"><span data-stu-id="26d7e-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="26d7e-116">Colaborador (pull e push).</span><span class="sxs-lookup"><span data-stu-id="26d7e-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="26d7e-117">Proprietário (pull, push e atribuir funções a outros usuários).</span><span class="sxs-lookup"><span data-stu-id="26d7e-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="26d7e-118">Acesso anônimo não está disponível em Registros de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="26d7e-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="26d7e-119">Para imagens públicas, você pode usar o [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="26d7e-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="26d7e-120">É possível atribuir várias entidades de serviço a um registro, o que permite definir acesso para diferentes usuários ou aplicativos.</span><span class="sxs-lookup"><span data-stu-id="26d7e-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="26d7e-121">As entidades de serviço também permitem conectividade “sem periféricos” a um registro em cenários de desenvolvedor ou DevOps, como nos seguintes exemplos:</span><span class="sxs-lookup"><span data-stu-id="26d7e-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="26d7e-122">Implantações de contêiner de um registro para sistemas de orquestração, incluindo DC/OS, Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="26d7e-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="26d7e-123">Também é possível efetuar pull de registros de contêiner para serviços do Azure relacionados, como [Serviço de Contêiner](../container-service/index.yml), [Serviço de Aplicativo](../app-service/index.md), [Lote](../batch/index.md) e [Service Fabric](/azure/service-fabric/), entre outros.</span><span class="sxs-lookup"><span data-stu-id="26d7e-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="26d7e-124">Soluções de integração e implantação contínuas (como Visual Studio Team Services ou Jenkins) que criam imagens de contêiner e as envia por push para um registro.</span><span class="sxs-lookup"><span data-stu-id="26d7e-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="26d7e-125">Conta de administrador</span><span class="sxs-lookup"><span data-stu-id="26d7e-125">Admin account</span></span>
<span data-ttu-id="26d7e-126">Com cada registro que você cria, uma conta de administrador é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="26d7e-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="26d7e-127">Por padrão, a conta está desabilitada, mas você pode habilitá-la e gerenciar as credenciais, por exemplo, por meio do [portal](container-registry-get-started-portal.md#manage-registry-settings) ou usando os [comandos da CLI 2.0 do Azure](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="26d7e-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="26d7e-128">Cada conta do administrador é fornecida com duas senhas, que podem ser regeneradas.</span><span class="sxs-lookup"><span data-stu-id="26d7e-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="26d7e-129">As duas senhas permitem manter conexões com o registro usando uma senha enquanto a outra senha é regenerada.</span><span class="sxs-lookup"><span data-stu-id="26d7e-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="26d7e-130">Se a conta estiver habilitada, você poderá passar o nome de usuário e a senha para o comando `docker login` para autenticação básica no registro.</span><span class="sxs-lookup"><span data-stu-id="26d7e-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="26d7e-131">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="26d7e-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="26d7e-132">A conta de administrador destina-se um único usuário para acessar o registro, principalmente para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="26d7e-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="26d7e-133">Não é recomendável compartilhar as credenciais da conta de administrador com outros usuários.</span><span class="sxs-lookup"><span data-stu-id="26d7e-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="26d7e-134">Todos os usuários aparecem como um único usuário no registro.</span><span class="sxs-lookup"><span data-stu-id="26d7e-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="26d7e-135">Alterar ou desabilitar essa conta desabilita o acesso ao registro para todos os usuários que usam as credenciais.</span><span class="sxs-lookup"><span data-stu-id="26d7e-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="26d7e-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26d7e-136">Next steps</span></span>
* <span data-ttu-id="26d7e-137">[Enviar por push sua primeira imagem usando a CLI do Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="26d7e-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="26d7e-138">Para saber mais sobre a autenticação na visualização do Registro de Contêiner, confira a [postagem no blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="26d7e-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
