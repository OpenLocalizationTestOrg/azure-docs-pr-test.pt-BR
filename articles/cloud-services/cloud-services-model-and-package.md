---
title: "aaaWhat é um modelo de serviço de nuvem e o pacote | Microsoft Docs"
description: "Descreve o modelo de serviço de nuvem hello (. csdef,. cscfg) e o pacote (. cspkg) no Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>O que é o modelo de serviço de nuvem hello e como empacotá-lo?
Um serviço de nuvem é criado de três componentes, definição de serviço Olá *(. csdef)*, Olá a configuração de serviço *(. cscfg)*e um pacote de serviço *(. cspkg)*. Ambos os Olá **servicedefinition. Csdef** e **ServiceConfig.cscfg** arquivos são baseados em XML e descrevem a estrutura de saudação do serviço de nuvem hello e como ele é configurado; coletivamente chamados de modelo de saudação. Olá **ServicePackage.cspkg** é um arquivo zip que é gerado a partir Olá **servicedefinition. Csdef** e entre outras coisas, contém todas as dependências de binário Olá necessário. O Azure cria um serviço de nuvem de ambos os Olá **ServicePackage.cspkg** e hello **ServiceConfig.cscfg**.

Quando o serviço de nuvem Olá estiver em execução no Azure, você pode reconfigurá-lo por meio de saudação **ServiceConfig.cscfg** arquivo, mas você não pode alterar a definição de saudação.

## <a name="what-would-you-like-tooknow-more-about"></a>O que você gostaria que tooknow mais sobre?
* Desejo tooknow mais sobre Olá [servicedefinition. Csdef](#csdef) e [ServiceConfig.cscfg](#cscfg) arquivos.
* Já sei sobre isso, dê-me [alguns exemplos](#next-steps) sobre o que posso configurar.
* Desejo Olá toocreate [ServicePackage.cspkg](#cspkg).
* Estou usando o Visual Studio e desejo...
  * [Criar um serviço de nuvem][vs_create]
  * [Reconfigurar um serviço de nuvem existente][vs_reconfigure]
  * [Implantar um projeto do serviço de nuvem][vs_deploy]
  * [Área de trabalho remota em uma instância de serviço de nuvem][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Olá **servicedefinition. Csdef** arquivo Especifica configurações de saudação que são usadas pelo Azure tooconfigure um serviço de nuvem. Olá [esquema de definição de serviço do Azure (arquivo. csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fornece o formato permitido Olá para um arquivo de definição de serviço. Olá, exemplo a seguir mostra as configurações de saudação que podem ser definidas para Olá Web e funções de trabalho:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Você pode consultar toohello [esquema de definição de serviço](https://msdn.microsoft.com/library/azure/ee758711.aspx) para melhor compreensão de esquema XML, Olá usada aqui, no entanto, aqui está uma breve explicação de alguns dos elementos de saudação:

**Sites**  
Contém definições de saudação para sites ou aplicativos web hospedados no IIS7.

**InputEndpoints**  
Contém definições de saudação para pontos de extremidade que usou o serviço de nuvem de saudação toocontact.

**InternalEndpoints**  
Contém as definições de saudação para pontos de extremidade que são usados por toocommunicate de instâncias de função com o outro.

**ConfigurationSettings**  
Contém as definições de configuração Olá para recursos de uma função específica.

**Certificados**  
Contém definições de saudação para certificados que são necessários para uma função. o exemplo de código anterior Olá mostra um certificado que é usado para a configuração de saudação do Azure Connect.

**LocalResources**  
Contém definições de saudação para recursos de armazenamento local. Um recurso de armazenamento local é um diretório reservado no sistema de arquivos de saudação da máquina virtual de saudação no qual uma instância de uma função está em execução.

**Imports**  
Contém definições de saudação para módulos importados. o exemplo de código anterior Olá mostra módulos Olá para Conexão de área de trabalho remota e o Azure Connect.

**Inicialização**  
Contém tarefas que são executadas quando a função hello for iniciada. Olá tarefas são definidas em um arquivo executável ou. cmd.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
configuração de saudação de configurações de saudação para seu serviço de nuvem é determinada pelos valores Olá Olá **ServiceConfiguration** arquivo. Você especifica o número de saudação de instâncias que você deseja toodeploy para cada função nesse arquivo. valores de Olá Olá as definições de configuração que você definiu no arquivo de definição de serviço Olá são adicionados toohello arquivo de configuração de serviço. impressões digitais de saudação para qualquer certificado de gerenciamento que estão associado com o serviço de nuvem Olá também são adicionadas toohello arquivo. Olá [esquema de configuração de serviço do Azure (arquivo. cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fornece o formato permitido Olá para um arquivo de configuração do serviço.

Olá arquivo de configuração de serviço não é fornecido com o aplicativo hello, mas é tooAzure carregado como um arquivo separado e é usado tooconfigure hello serviço de nuvem. Você pode carregar um novo arquivo de configuração de serviço sem reimplantar o serviço de nuvem. os valores de configuração Olá Olá serviço de nuvem podem ser alterados enquanto o serviço de nuvem hello está em execução. Olá, exemplo a seguir mostra as definições de configuração de saudação que podem ser definidas para Olá Web e funções de trabalho:

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Você pode consultar toohello [esquema de configuração de serviço](https://msdn.microsoft.com/library/azure/ee758710.aspx) para melhor compreensão Olá esquema XML usado aqui, no entanto, aqui está uma breve explicação de elementos de saudação:

**Instâncias**  
Configura o número de saudação de instâncias em execução para a função hello. tooprevent sua nuvem de serviço de fique indisponível durante atualizações, é recomendável que você implantar mais de uma instância de suas funções para a web. Ao implantar mais de uma instância, você está aderindo diretrizes toohello Olá [contrato de nível de serviço de computação do Azure (SLA)](http://azure.microsoft.com/support/legal/sla/), que garante 99,95% de conectividade externa para funções da Internet quando duas ou mais funções instâncias são implantadas para um serviço.

**ConfigurationSettings**  
Define as configurações de saudação para Olá instâncias em execução para uma função. nome de saudação do hello `<Setting>` elementos devem coincidir com as definições de configuração Olá no arquivo de definição de serviço hello.

**Certificados**  
Configura os certificados de saudação que são usados pelo serviço de saudação. o exemplo de código anterior Olá mostra como toodefine Olá certificado para o módulo RemoteAccess de saudação. Olá valor Olá *impressão digital* atributo deve ser definido como impressão digital de toohello de saudação toouse de certificado.

<p/>

> [!NOTE]
> pode ser adicionado a impressão digital de saudação do certificado de saudação toohello arquivo de configuração usando um editor de texto. Ou, Olá valor pode ser adicionado em Olá **certificados** guia da saudação **propriedades** página da função hello no Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Definindo as portas para instâncias de função
O Azure permite apenas uma função de web tooa de ponto de entrada. Isso significa que todo o tráfego ocorre por meio de um endereço IP. Você pode configurar seu sites tooshare uma porta Configurando Olá host cabeçalho toodirect Olá solicitação toohello local correto. Você também pode configurar as portas do aplicativos toolisten toowell conhecidas no endereço IP hello.

Olá, exemplo a seguir mostra a configuração Olá para uma função web com um aplicativo web e o site. Olá site está configurado como local de entrada hello padrão na porta 80 e aplicativos da web de saudação são solicitações tooreceive configurado de um cabeçalho de host alternativo que é chamado de "mail.mysite.cloudapp.net".

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Alterando a configuração de saudação de uma função
Você pode atualizar a configuração de saudação de seu serviço de nuvem enquanto está em execução no Azure, sem colocar offline o serviço de saudação. toochange informações de configuração, você pode carregar um novo arquivo de configuração ou editar Olá arquivo de configuração de colocar e aplicá-lo tooyour executando o serviço. Olá alterações a seguir podem ser feitas toohello configuração de um serviço:

* **Alterando os valores hello definições de configuração**  
  Quando uma configuração de alterações, de configuração uma instância de função pode escolher tooapply Olá alteração Olá instância está online ou toorecycle Olá instância normalmente e aplique a alteração de saudação enquanto Olá instância está offline.
* **A alteração de topologia do serviço de saudação de instâncias de função**  
  As alterações da topologia não afetam as instâncias em execução, exceto quando uma instância está sendo removida. Todas as instâncias restantes geralmente não é necessário toobe reciclado; No entanto, você pode escolher toorecycle instâncias de função na alteração de topologia de tooa de resposta.
* **Alterando a impressão digital do certificado Olá**  
   Somente é possível atualizar um certificado quando uma instância de função está offline. Se um certificado for adicionado, excluído ou alterado enquanto uma instância de função estiver online, o Azure normalmente usa certificados de Olá Olá instância tooupdate off-line e colocá-lo novamente online após a conclusão da alteração de saudação.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Tratando alterações de configuração com eventos de tempo de execução do serviço
Olá [biblioteca de tempo de execução do Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclui Olá [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, que fornece classes para interagir com hello ambiente do Azure de uma função. Olá [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe define Olá eventos que são disparados antes e após uma alteração de configuração a seguir:

* **[Alterando](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) eventos**  
  Isso ocorre antes que alterações de configuração de saudação tooa aplicada a instância especificada de uma função fornecendo tootake uma chance para instâncias de função hello, se necessário.
* **[Evento](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) alterado**  
  Ocorre após a alteração de configuração Olá tooa aplicada a instância especificada de uma função.

> [!NOTE]
> Como alterações de certificado sempre usa instâncias de saudação de uma função off-line, elas não geram eventos de saudação Changing ou RoleEnvironment.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy um aplicativo como um serviço de nuvem no Azure, você deve primeiro aplicativo hello de pacote no formato apropriado de saudação. Você pode usar o hello **CSPack** ferramenta de linha de comando (instalado com hello [SDK do Azure](https://azure.microsoft.com/downloads/)) toocreate arquivo de pacote hello como uma alternativa tooVisual Studio.

**CSPack** usa Olá conteúdo da saudação serviço definição serviço de configuração toodefine Olá conteúdo do arquivo de pacote de saudação. **CSPack** gera um arquivo de pacote de aplicativo (. cspkg) que você pode carregar tooAzure usando Olá [portal do Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Por padrão, o pacote de saudação é chamado `[ServiceDefinitionFileName].cspkg`, mas você pode especificar um nome diferente usando Olá `/out` opção de **CSPack**.

**CSPack** está localizado em  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (no windows) está disponível executando Olá **Prompt de comando do Microsoft Azure** atalho que é instalado com o SDK de saudação.  
> 
> Execute o programa de CSPack.exe de saudação por si só toosee documentação sobre todas as opções possíveis hello e comandos.
> 
> 

<p />

> [!TIP]
> Executar seu serviço de nuvem localmente no hello **emulador de computação do Microsoft Azure**, use Olá **/copyonly** opção. Esta opção copia arquivos binários de saudação para layout de diretório Olá aplicativo tooa do qual eles podem ser executados no emulador de computação hello.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Comando de exemplo toopackage um serviço de nuvem
Olá, exemplo a seguir cria um pacote de aplicativo que contém informações de saudação para uma função web. comando Olá Especifica Olá toouse de arquivo de definição de serviço, diretório Olá onde os arquivos binários podem ser encontrado e Olá o nome do arquivo de pacote de saudação.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Se o aplicativo hello contém uma função web e uma função de trabalho, hello comando a seguir é usado:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Onde as variáveis de saudação são definidas da seguinte maneira:

| Variável | Valor |
| --- | --- |
| \[DirectoryName\] |Olá subdiretório no diretório do projeto Olá raiz que contém o arquivo. csdef Olá Olá projeto do Azure. |
| \[ServiceDefinition\] |nome de saudação do arquivo de definição de serviço hello. Por padrão, esse arquivo é chamado de ServiceDefinition.csdef. |
| \[OutputFileName\] |nome Olá Olá gerou o arquivo de pacote. Normalmente, isso é definido toohello nome do aplicativo hello. Se nenhum nome de arquivo for especificado, o pacote de aplicativo hello é criado como \[ApplicationName\]. cspkg. |
| \[RoleName\] |nome de saudação da função de saudação conforme definido no arquivo de definição de serviço hello. |
| \[RoleBinariesDirectory] |local de saudação de arquivos binários para função Olá Olá. |
| \[VirtualPath\] |diretórios físicos de saudação para cada caminho virtual definido na seção de Sites de saudação da definição de serviço hello. |
| \[PhysicalPath\] |Olá diretórios físicos do conteúdo de saudação de cada caminho virtual definido no nó do site Olá da definição de serviço hello. |
| \[RoleAssemblyName\] |nome de saudação do arquivo binário Olá função hello. |

## <a name="next-steps"></a>Próximas etapas
Estou criando um pacote de serviço de nuvem e desejo...

* [Configurar área de trabalho remota para uma instância de serviço de nuvem][remotedesktop]
* [Implantar um projeto do serviço de nuvem][deploy]

Estou usando o Visual Studio e desejo...

* [Criar um novo serviço de nuvem][vs_create]
* [Reconfigurar um serviço de nuvem existente][vs_reconfigure]
* [Implantar um projeto do serviço de nuvem][vs_deploy]
* [Configurar área de trabalho remota para uma instância de serviço de nuvem][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
