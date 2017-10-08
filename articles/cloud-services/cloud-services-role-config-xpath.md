---
title: "roteiro do aaaCloud serviços de função config XPath | Microsoft Docs"
description: "Olá várias configurações de XPath, que você poderá usar as configurações de tooexpose de configuração de função serviço de nuvem hello como uma variável de ambiente."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Expor as definições de configuração da função como uma variável de ambiente com o XPath
No trabalho de serviço de nuvem hello ou arquivo de definição de serviço de função da web, você pode expor os valores de configuração de tempo de execução como variáveis de ambiente. Olá valores de XPath a seguir têm suporte (que correspondem a valores de tooAPI).

Esses valores de XPath também estão disponíveis por meio de saudação [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteca. 

## <a name="app-running-in-emulator"></a>Aplicativo em execução no emulador
Indica que o aplicativo hello está sendo executado no emulador de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| Código |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>ID de Implantação
Recupera a ID de implantação de saudação para instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| Código |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>ID de Função
Recupera Olá ID da função atual para a instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| Código |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Domínio de atualização
Recupera o domínio de atualização de saudação da instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| Código |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Domínios de falha
Recupera o domínio de falha de saudação da instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| Código |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Nome da função
Recupera o nome da função hello de instâncias de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| Código |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Definição de configuração
Recupera valor Olá Olá especificado de configuração.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| Código |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Caminho do armazenamento local
Recupera o caminho de armazenamento local de saudação da instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| Código |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>Tamanho do armazenamento local
Recupera o tamanho de saudação do armazenamento local Olá instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| Código |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Protocolo do ponto de extremidade
Recupera o protocolo de ponto de extremidade de saudação para instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| Código |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>IP do ponto de extremidade
Obtém Olá especificado o endereço IP do ponto de extremidade.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| Código |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>Porta do ponto de extremidade
Recupera a porta do ponto de extremidade Olá para instância de saudação.

| Tipo | Exemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| Código |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>Exemplo
Aqui está um exemplo de uma função de trabalho que cria uma tarefa de inicialização com uma variável de ambiente denominada `TestIsEmulated` definir toohello [ @emulated valor xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [ServiceConfiguration](cloud-services-model-and-package.md#serviceconfigurationcscfg) arquivo.

Crie um pacote [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .

Habilite a [área de trabalho remota](cloud-services-role-enable-remote-desktop.md) para uma função.

