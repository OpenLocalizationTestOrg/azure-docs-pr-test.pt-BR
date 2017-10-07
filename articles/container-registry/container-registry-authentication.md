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
# <a name="authenticate-with-a-private-docker-container-registry"></a>Autenticar com um Registro de contêiner privado do Docker
toowork com imagens de contêiner em um registro de contêiner do Azure, que você faça logon usando Olá `docker login` comando. Você pode fazer logon usando uma **[entidade de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou uma **conta de administrador** específica do registro. Este artigo fornece mais detalhes sobre essas identidades.



## <a name="service-principal"></a>Entidade de serviço

Você pode [atribuir uma entidade de serviço](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registro e usá-lo para a autenticação básica do Docker. Usar uma entidade de serviço é recomendado para a maioria dos cenários. Fornecer ID do aplicativo hello e a senha da saudação serviço principal toohello `docker login` de comando, conforme mostrado no exemplo a seguir de saudação:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Depois de conectado, Docker armazena em cache as credenciais Olá, que exige o ID do aplicativo hello. tooremember

> [!TIP]
> Se desejar, você pode regenerar senha saudação de uma entidade de serviço executando Olá `az ad sp reset-credentials` comando.
>


Permitir que as entidades de serviço [acesso baseado em função](../active-directory/role-based-access-control-configure.md) tooa registro. As funções disponíveis são:
  * Leitor (acesso somente de pull).
  * Colaborador (pull e push).
  * Proprietário (pull, push e atribuir funções tooother usuários).

Acesso anônimo não está disponível em Registros de Contêiner do Azure. Para imagens públicas, você pode usar o [Docker Hub](https://docs.docker.com/docker-hub/).

Você pode atribuir várias entidades de serviço do registro tooa, o que permite a você acesso toodefine para diferentes usuários ou aplicativos. Entidades de serviço também habilitar registro tooa conectividade "sem cabeçalho" desenvolvedor ou cenários de DevOps como Olá exemplos a seguir:

  * Implantações do contêiner de sistemas de tooorchestration de registro, incluindo DC/OS, Docker Swarm e Kubernetes. Você também pode extrair contêiner registros toorelated serviços do Azure como [serviço de contêiner](../container-service/index.yml), [do serviço de aplicativo](../app-service/index.md), [lote](../batch/index.md), [Service Fabric](/azure/service-fabric/)e outros.

  * Contínua integração e implantação de soluções (como o Visual Studio Team Services ou Jenkins) criar imagens de contêiner e enviá-las tooa registro.





## <a name="admin-account"></a>Conta de administrador
Com cada registro que você cria, uma conta de administrador é criada automaticamente. Por padrão a conta hello está desabilitada, mas você pode habilitá-lo e gerenciar credenciais de hello, por exemplo por meio da saudação [portal](container-registry-get-started-portal.md#manage-registry-settings) ou usando Olá [comandos do Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Cada conta do administrador é fornecida com duas senhas, que podem ser regeneradas. as duas senhas de saudação permitem toomaintain do registro toohello de conexões usando uma senha enquanto você regenera Olá outra senha. Se Olá conta estiver habilitada, você pode passar o nome de usuário de saudação e a senha toohello `docker login` comando de registro de toohello de autenticação básica. Por exemplo:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> conta de administrador Olá destina-se um único usuário tooaccess saudação do registro, principalmente para fins de teste. Não é recomendável credenciais da conta de administrador tooshare Olá entre outros usuários. Todos os usuários aparecem como um registro de toohello de usuário único. Alterar ou desabilitar esta conta desabilita o acesso de registro para todos os usuários que usam credenciais hello.
>


### <a name="next-steps"></a>Próximas etapas
* [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md).
* Para obter mais informações sobre a autenticação na visualização de registro de contêiner hello, consulte Olá [postagem de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
