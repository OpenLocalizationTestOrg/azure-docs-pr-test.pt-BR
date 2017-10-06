---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Criar um registro de contêiner do Docker privado usando hello Azure PowerShell
Usar comandos em [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate um registro de contêiner e gerenciar suas configurações de seu computador com Windows. Você também pode criar e gerenciar registros de contêiner usando Olá [portal do Azure](container-registry-get-started-portal.md), Olá [CLI do Azure](container-registry-get-started-azure-cli.md), ou programaticamente com hello registro de contêiner [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Para o plano de fundo e conceitos, consulte [Olá visão geral](container-registry-intro.md)
* Para obter uma lista completa dos cmdlets com suporte, consulte [Cmdlets de gerenciamento do Registro de Contêiner do Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Pré-requisitos
* **O Azure PowerShell**: tooinstall e começar com o Azure PowerShell, consulte Olá [instruções de instalação](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Faça logon no tooyour assinatura do Azure executando `Login-AzureRMAccount`. Para obter mais informações, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Grupo de recursos**: crie um [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) antes de criar um registro de contêiner ou usar um grupo de recursos existente. Verifique se o grupo de recursos hello está em um local onde está o serviço de registro de contêiner de saudação [disponível](https://azure.microsoft.com/regions/services/). toocreate um grupo de recursos usando o PowerShell do Azure, consulte [Olá referência do PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Conta de armazenamento** (opcional): criar um padrão Azure [conta de armazenamento](../storage/common/storage-introduction.md) tooback registro de contêiner de saudação em Olá mesmo local. Se você não especificar uma conta de armazenamento ao criar um registro com `New-AzureRMContainerRegistry`, comando Olá criará um para você. toocreate um armazenamento de conta usando o PowerShell, consulte [Olá referência do PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Atualmente, não há suporte para o Armazenamento Premium.
* **Entidade de serviço** (opcional): quando você cria um registro com o PowerShell, por padrão, ele não é configurado para acesso. Dependendo de suas necessidades, você pode atribuir um registro de tooa principal de serviço existente do Active Directory do Azure ou criar e atribuir um novo. Como alternativa, você pode habilitar a conta de usuário admin do registro hello. Consulte as seções Olá posteriormente neste artigo. Para obter mais informações sobre o acesso de registro, consulte [autenticar com o registro de contêiner Olá](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Criar um registro de contêiner
Executar Olá `New-AzureRMContainerRegistry` comando toocreate um registro de contêiner.

> [!TIP]
> Ao criar um registro, especifique um nome de domínio de nível superior exclusivo que contenha apenas letras e números. nome do registro de saudação nos exemplos de saudação é `MyRegistry`, mas substitua um nome exclusivo.
>
>

Olá usa Olá registro de contêiner toocreate mínimo de parâmetros de comando a seguir `MyRegistry` no grupo de recursos de saudação `MyResourceGroup` em Olá Centro Sul dos EUA local:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` é opcional. Se não for especificado, uma conta de armazenamento é criada com um nome que consiste do nome do registro de saudação e um carimbo de hora Olá especificado o grupo de recursos.

## <a name="assign-a-service-principal"></a>Atribuir uma entidade de serviço
Usar comandos de PowerShell tooassign um Azure Active Directory [entidade de serviço](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registro. Hello entidade de serviço nesses exemplos é designada como Olá proprietário, mas você pode atribuir [outras funções](../active-directory/role-based-access-control-configure.md) se desejar.

### <a name="create-a-service-principal"></a>Criar uma entidade de serviço
Olá comando a seguir, uma nova entidade de serviço é criada. Especifique uma senha forte com hello `-Password` parâmetro.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Atribuir uma entidade de serviço nova ou existente
Você pode atribuir um novo ou um registro de tooa principal de serviço existente. tooassign-proprietário função acessar toohello o registro, execute um toohello semelhante do comando exemplo a seguir:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Entrar no registro toohello com a entidade de serviço Olá
Depois de atribuir o registro de toohello principal do serviço hello, você pode entrar usando Olá comando a seguir:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Gerenciar credenciais de administrador
Uma conta de administrador é automaticamente criada para cada registro de contêiner e é desabilitada por padrão. Olá exemplos a seguir mostram comandos do PowerShell credenciais de administrador toomanage Olá para o registro de contêiner.

### <a name="obtain-admin-user-credentials"></a>Obter credenciais de usuário administrador
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Habilitar o usuário administrador para um registro existente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Desabilitar o usuário administrador para um registro existente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Próximas etapas
* [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
