---
title: registro de Docker privado aaaCreate - portal do Azure | Microsoft Docs
description: "Começar a criar e gerenciar registros privados de contêiner do Docker com hello portal do Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Criar um registro de contêiner do Docker privado usando Olá portal do Azure
Use Olá toocreate portal do Azure um registro de contêiner e gerenciar suas configurações. Você também pode criar e gerenciar registros de contêiner usando Olá [comandos 2.0 do CLI do Azure](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) ou programaticamente com hello registro de contêiner [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).

Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Criar um registro de contêiner
1. Em Olá [portal do Azure](https://portal.azure.com), clique em **+ novo**.
2. Marketplace de saudação de pesquisa para **registro de contêiner do Azure**.
3. Selecione **Registro de Contêiner do Azure** com o editor **Microsoft**.
    ![Serviço de registro de contêiner no Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Clique em **Criar**. Olá **registro de contêiner do Azure** folha é exibida.

    ![Configurações de registro de contêiner](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Em Olá **registro de contêiner do Azure** folha, digite Olá informações a seguir. Clique em **Criar** quando terminar.

    a. **Nome do registro**: um nome de domínio de nível superior exclusivo para o registro específico. Neste exemplo, o nome de registro de saudação é *myRegistry01*, mas substitua um nome exclusivo. nome de saudação pode conter apenas letras e números.

    b. **Grupo de recursos**: selecione uma existente [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.

    c. **Local**: selecione um local de data center do Azure onde está o serviço Olá [disponível](https://azure.microsoft.com/regions/services/), como **Centro Sul dos EUA**.

    d. **O usuário administrador**: se desejar, habilite um registro de saudação de tooaccess de usuário admin. Você pode alterar essa configuração após a criação do registro de saudação.

      > [!IMPORTANT]
      > Além disso tooproviding acesso por meio de uma conta de usuário administrador, registros de contêiner oferecem suporte à autenticação com o apoio de entidades de serviço do Active Directory do Azure. Para obter mais informações e considerações, confira [Autenticar em um registro de contêiner](container-registry-authentication.md).
      >

    e. **Conta de armazenamento**: usar saudação padrão configuração toocreate uma [conta de armazenamento](../storage/common/storage-introduction.md), ou selecione uma conta de armazenamento existente na Olá mesmo local. Atualmente, não há suporte para o Armazenamento Premium.

## <a name="manage-registry-settings"></a>Gerenciar configurações do registro
Depois de criar o registro de hello, localize Olá as configurações do registro iniciando em hello **registros de contêiner** folha no portal de saudação. Por exemplo, talvez seja necessário Olá toolog de configurações no registro tooyour ou pode ser desejável tooenable ou desabilitar o usuário de administrador hello.

1. Em Olá **registros de contêiner** folha, clique em nome de saudação do registro.

    ![Folha de registro de contêiner](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Clique em configurações de acesso toomanage **chave de acesso**.

    ![Acesso ao registro de contêiner](./media/container-registry-get-started-portal/container-registry-access.png)
3. Observe Olá configurações a seguir:

   * **Servidor de logon** -nome totalmente qualificado do hello usar toolog no registro toohello. Neste exemplo, é `myregistry01.azurecr.io`.
   * **O usuário administrador** - alternar tooenable ou desabilitar a conta de usuário admin do registro hello.
   * **Nome de usuário** e **senha** -Olá credenciais da conta de usuário de administrador hello (se habilitado) você pode usar toolog no registro toohello. Opcionalmente, você pode regenerar senhas hello. As duas senhas são criadas para que você pode manter registro de toohello conexões usando uma senha enquanto você regenera Olá outra senha. em vez disso, consulte tooauthenticate com uma entidade de serviço [autenticar com um registro de contêiner do Docker particular](container-registry-authentication.md).

## <a name="next-steps"></a>Próximas etapas
* [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
