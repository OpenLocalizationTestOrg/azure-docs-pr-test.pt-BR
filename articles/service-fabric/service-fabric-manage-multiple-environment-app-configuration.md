---
title: "aaaManage vários ambientes na malha do serviço | Microsoft Docs"
description: "Aplicativos de malha do serviço podem ser executados em clusters que variam em tamanho de um toothousands de máquina de máquinas. Em alguns casos, você desejará tooconfigure seu aplicativo diferentes para esses ambientes variados. Este artigo aborda como parâmetros de aplicativo diferente de toodefine por ambiente."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Gerenciar parâmetros do aplicativo para vários ambientes
Você pode criar clusters de malha do serviço do Azure, usando qualquer parte de um toomany milhares de máquinas. Enquanto os binários de aplicativo podem ser executado sem modificação nesse amplo espectro de ambientes, você geralmente deseja tooconfigure Olá aplicativo diferente, dependendo do número de saudação de máquinas que você estiver implantando em.

Como um exemplo simples, considere a `InstanceCount` para um serviço sem estado. Quando você estiver executando aplicativos no Azure, geralmente convém tooset este toohello especial valor de parâmetro "-1". Essa configuração garante que o serviço está em execução em cada nó no cluster hello (ou todos os nós no tipo de nó Olá se você tiver definido uma restrição de posicionamento). No entanto, essa configuração não é adequada para um cluster de computador único porque você não pode ter vários processos escutando Olá mesmo ponto de extremidade em um único computador. Em vez disso, você normalmente define `InstanceCount` muito "1".

## <a name="specifying-environment-specific-parameters"></a>Especificando parâmetros específicos do ambiente
problema de configuração de toothis Olá solução é um conjunto de serviços padrão com parâmetros e arquivos de parâmetro de aplicativo que preencham os valores de parâmetro para um determinado ambiente. Serviços padrão e parâmetros do aplicativo são configurados no aplicativo hello e manifestos do serviço. Olá definição de esquema para arquivos ServiceManifest.xml e ApplicationManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Serviços padrão
Os aplicativos do Service Fabric são compostos de uma coleção de instâncias de serviço. Enquanto é possível toocreate um aplicativo vazio e, em seguida, criar dinamicamente todas as instâncias de serviço, a maioria dos aplicativos têm um conjunto de serviços principais que sempre deve ser criada quando o aplicativo hello é instanciado. Esses são chamados tooas "serviços padrão". Eles são especificados no manifesto de aplicativo hello, com espaços reservados para a configuração de per ambiente incluído entre colchetes:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Cada Olá parâmetros nomeado deve ser definida no elemento de parâmetros Olá Olá do manifesto do aplicativo:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

atributo DefaultValue de saudação especifica Olá valor toobe usado na ausência de saudação de um parâmetro mais específicas para um determinado ambiente.

> [!NOTE]
> Nem todos os parâmetros da instância de serviço são adequados para a configuração por ambiente. O exemplo hello acima, Olá LowKey e HighKey valores para o esquema de particionamento do serviço Olá são definidos explicitamente para todas as instâncias do serviço de saudação desde que o intervalo de partição Olá é uma função de saudação do domínio de dados, não o ambiente hello.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Definições de configuração de serviço por ambiente
Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md) habilita serviços tooinclude pacotes de configuração que contém pares chave-valor personalizados que podem ser lidos em tempo de execução. os valores Hello dessas configurações também podem ser diferenciados pelo ambiente especificando um `ConfigOverride` no manifesto de aplicativo hello.

Suponha que você tenha Olá após a configuração no arquivo Config\Settings.xml Olá Olá `Stateful1` serviço:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride esse valor para um par de aplicativo/ambiente específico, crie um `ConfigOverride` quando você importa o manifesto do serviço Olá no manifesto de aplicativo hello.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Esse parâmetro pode então ser configurado pelo ambiente como mostrado acima. Você pode fazer isso declará-la na seção de parâmetros de saudação do manifesto de aplicativo hello e especificando valores específicos de ambiente nos arquivos de parâmetro de aplicativo hello.

> [!NOTE]
> No caso de saudação de definições de configuração de serviço, há três locais em que o valor de saudação de uma chave pode ser definido: pacote de configuração de serviço hello, o manifesto do aplicativo hello e arquivo de parâmetro de aplicativo hello. Malha do serviço será sempre escolher Olá parâmetro do arquivo de aplicativo primeiro (se especificado), em seguida, Olá manifesto do aplicativo e hello, por fim, o pacote de configuração.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Configurando e usando variáveis de ambiente 
Você pode especificar e definir variáveis de ambiente no arquivo ServiceManifest.xml de saudação e, em seguida, substituir no arquivo de ApplicationManifest.xml Olá em uma base por instância.
Olá exemplo a seguir mostra duas variáveis de ambiente, um com um valor definido e outros Olá é substituído. Você pode usar parâmetros de valores de variáveis de ambiente tooset em Olá mesma forma que eles foram usados para substituições de configuração do aplicativo.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
variáveis de ambiente toooverride Olá no hello ApplicationManifest.xml, pacote de códigos de saudação de referência em Olá ServiceManifest com hello `EnvironmentOverrides` elemento.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Quando Olá serviço instância nomeada é criado, você pode acessar variáveis de ambiente de saudação do código. Por exemplo, no c# Faça a seguir Olá

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Variáveis de ambiente do Service Fabric
O Service Fabric tem variáveis de ambiente internas definidas para cada instância de serviço. Olá lista completa de variáveis de ambiente é abaixo, onde hello aqueles em negrito são Olá aquelas que você usará em seu serviço, Olá outros que está sendo usada pelo tempo de execução do Service Fabric. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[YourServiceName]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Olá belows de código mostra como toolist Olá variáveis de ambiente do Service Fabric
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Olá, estes são exemplos de variáveis de ambiente para um tipo de aplicativo chamado `GuestExe.Application` com um tipo de serviço chamado `FrontEndService` quando executado em sua máquina de desenvolvimento local.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>Arquivos de parâmetros de aplicativo
projeto de aplicativo do Service Fabric Olá pode incluir um ou mais arquivos de parâmetro de aplicativo. Cada uma delas define valores específicos de saudação para parâmetros de saudação que são definidos no manifesto de aplicativo hello:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Por padrão, um novo aplicativo inclui três arquivos de parâmetro de aplicativo, chamados Local.1Node.xml, Local.5Node.xml e Cloud.xml:

![Arquivos de parâmetros de aplicativo no Gerenciador de Soluções][app-parameters-solution-explorer]

toocreate um arquivo de parâmetro, simplesmente copie e cole um existente e dê a ele um novo nome.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Identificando parâmetros específicos do ambiente durante a implantação
No momento da implantação, você precisa toochoose Olá parâmetro apropriado arquivo tooapply com seu aplicativo. Você pode fazer isso por meio da caixa de diálogo de publicação de saudação no Visual Studio ou PowerShell.

### <a name="deploy-from-visual-studio"></a>Implantar com o Visual Studio
Você pode escolher na lista de saudação de arquivos de parâmetros disponíveis quando você publicar seu aplicativo no Visual Studio.

![Escolha um arquivo de parâmetro na caixa de diálogo de publicação Olá][publishdialog]

### <a name="deploy-from-powershell"></a>Implantar do PowerShell
Olá `Deploy-FabricApplication.ps1` script do PowerShell incluído no modelo de projeto de aplicativo hello aceita como um parâmetro de um perfil de publicação e Olá PublishProfile contém um arquivo de parâmetros de aplicativo de toohello de referência.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre alguns dos conceitos básicos de saudação que são abordados neste tópico, consulte Olá [visão geral técnica do Service Fabric](service-fabric-technical-overview.md). Para obter informações sobre outras funcionalidades de gerenciamento de aplicativo disponíveis no Visual Studio, confira [Gerenciar seus aplicativos do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
