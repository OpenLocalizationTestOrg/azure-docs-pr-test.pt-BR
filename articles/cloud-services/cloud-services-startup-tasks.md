---
title: "aaaRun tarefas de inicialização nos serviços de nuvem do Azure | Microsoft Docs"
description: "As tarefas de inicialização ajudam a preparar o ambiente de serviço de nuvem para seu aplicativo. Isso ensina como o trabalho de tarefas de inicialização e toomake-los"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Como as tarefas de inicialização tooconfigure e execução de um serviço de nuvem
Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função. Operações que convém tooperform incluem instalação de um componente, registrando componentes COM, chaves do registro de configuração ou iniciar um processo de execução longa.

> [!NOTE]
> Tarefas de inicialização não são aplicáveis tooVirtual máquinas, apenas tooCloud serviço Web e funções de trabalho.
> 
> 

## <a name="how-startup-tasks-work"></a>Como funcionam as tarefas de inicialização
Tarefas de inicialização são ações que são executadas antes de suas funções começam e são definidas em hello [servicedefinition. Csdef] arquivo usando Olá [tarefa] elemento dentro do hello [inicialização]elemento. Com frequência, as tarefas de inicialização são arquivos em lotes, mas elas também podem ser aplicativos de console ou arquivos em lotes que iniciam scripts do PowerShell.

Variáveis de ambiente transmitem informações em uma tarefa de inicialização e armazenamento local pode ser usado toopass informações fora de uma tarefa de inicialização. Por exemplo, uma variável de ambiente pode especificar o programa de tooa caminho Olá deseja tooinstall e arquivos podem ser gravados armazenamento toolocal que pode ser lidos posteriormente por suas funções.

Sua tarefa de inicialização pode registrar informações e o diretório de toohello de erros especificado pelo Olá **TEMP** variável de ambiente. Durante a tarefa de inicialização de Olá Olá **TEMP** variável de ambiente resolve toohello *c:\\recursos\\temp\\[guid]. [ rolename]\\RoleTemp* diretório quando em execução na nuvem hello.

As tarefas de inicialização também podem ser executadas várias vezes entre as reinicializações. Por exemplo, Olá inicialização tarefa será executada cada vez Olá função se recicla e a reciclagem de função não pode incluir sempre uma reinicialização. Tarefas de inicialização devem ser escritas de forma a permitir que eles toorun várias vezes sem problemas.

Tarefas de inicialização devem terminar com uma **errorlevel** (ou código de saída) de zero para Olá toocomplete de processo de inicialização. Se uma tarefa de inicialização termina com diferente de zero **errorlevel**, Olá função não será iniciada.

## <a name="role-startup-order"></a>Ordem de inicialização de função
Olá seguindo o procedimento de inicialização de função listas Olá no Azure:

1. Olá instância é marcada como **iniciando** e não recebe o tráfego.
2. Todas as tarefas de inicialização são executadas de acordo com tootheir **taskType** atributo.
   
   * Olá **simples** tarefas são executadas de forma síncrona, uma de cada vez.
   * Olá **em segundo plano** e **primeiro plano** tarefas são iniciadas de forma assíncrona, paralelas toohello tarefa de inicialização.  
     
     > [!WARNING]
     > O IIS pode não estar totalmente configurado durante a fase de tarefas de inicialização Olá no processo de inicialização hello, para que dados específicos de função podem não estar disponíveis. As tarefas de inicialização que exigem dados específicos da função devem usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. processo de host de função Hello é iniciado e Olá site é criado no IIS.
4. Olá [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método é chamado.
5. Olá instância é marcada como **pronto** e o tráfego é roteado toohello instância.
6. Olá [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método é chamado.

## <a name="example-of-a-startup-task"></a>Exemplo de uma tarefa de inicialização
Tarefas de inicialização são definidas no hello [servicedefinition. Csdef] arquivo, em Olá **tarefa** elemento. Olá **commandLine** atributo especifica o nome da saudação e parâmetros do lote de inicialização de saudação do arquivo ou no console de comando, hello **executionContext** atributo especifica o nível de privilégio de saudação de inicialização Olá tarefas e hello **taskType** atributo especifica como Olá tarefa será executada.

Neste exemplo, uma variável de ambiente **MyVersionNumber**, é criado para a tarefa de inicialização hello e defina o valor de toohello "**1.0.0.0**".

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

Em Olá exemplo a seguir, Olá **Startup.cmd** arquivo em lote grava linha hello "o hello current version is 1.0.0.0" arquivo de StartupLog.txt toohello no diretório de saudação especificado pela variável de ambiente TEMP hello. Olá `EXIT /B 0` linha garante que essa tarefa de inicialização Olá termina com um **errorlevel** igual a zero.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> No Visual Studio, Olá **copiar tooOutput diretório** propriedade para o arquivo em lotes de inicialização deve ser definida muito**copiar sempre** toobe-se de que o arquivo em lotes de inicialização esteja adequadamente implantado tooyour projeto no Azure (**approot\\bin** para funções da Web, e **approot** para funções de trabalho).
> 
> 

## <a name="description-of-task-attributes"></a>Descrição dos atributos da tarefa
Hello, a seguir descreve os atributos de saudação do hello **tarefa** elemento Olá [servicedefinition. Csdef] arquivo:

**linha de comando** -Especifica Olá a linha de comando para a tarefa de inicialização hello:

* comando Hello, com parâmetros de linha de comando opcional, que inicia a tarefa de inicialização de saudação.
* Geralmente, isso é Olá nome do arquivo de um arquivo em lotes. cmd ou. bat.
* tarefa de saudação é relativo toohello AppRoot\\pasta Bin para implantação de saudação. Variáveis de ambiente não são expandidas para determinar o caminho hello e da tarefa de saudação. Se a expansão de ambiente for necessária, você poderá criar um script .cmd pequeno que chame sua tarefa de inicialização.
* Pode ser um aplicativo de console ou um arquivo em lotes que inicie um [script do PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -Especifica o nível de privilégio Olá para tarefa de inicialização de saudação. nível de privilégio Olá pode ser limitado ou elevado:

* **limitado**  
  tarefa de inicialização de saudação é executado com hello mesmo privilégios como função hello. Olá quando **executionContext** atributo Olá [tempo de execução] elemento também é **limitado**, privilégios de usuário são usadas.
* **elevado**  
  tarefa de inicialização de saudação é executado com privilégios de administrador. Isso permite que as tarefas de inicialização tooinstall programas, faça as alterações de configuração do IIS, realizar alterações no registro e outras tarefas de nível de administrador sem aumentar o nível de privilégio de saudação da própria função hello.  

> [!NOTE]
> Olá nível de privilégio de uma tarefa de inicialização não precisa toobe Olá mesmo como função hello em si.
> 
> 

**taskType** -Especifica Olá forma uma tarefa de inicialização é executado.

* **simpless**  
  Tarefas são executadas de forma síncrona, uma de cada vez, em ordem de saudação especificado no hello [servicedefinition. Csdef] arquivo. Quando um **simples** tarefa de inicialização termina com um **errorlevel** de zero, em seguida Olá **simples** tarefa de inicialização é executada. Se houver mais **simples** tooexecute, tarefas de inicialização e a função hello em si será iniciada.   
  
  > [!NOTE]
  > Se hello **simples** tarefa termina com diferente de zero **errorlevel**, Olá instância será bloqueada. Subsequentes **simples** tarefas de inicialização e a função hello em si, não serão iniciado.
  > 
  > 
  
    tooensure o arquivo em lotes termina com um **errorlevel** de zero, execute o comando Olá `EXIT /B 0` final de saudação de seu processo de arquivo em lotes.
* **segundo plano**  
  Tarefas são executadas de forma assíncrona, em paralelo com a inicialização de saudação da função hello.
* **primeiro plano**  
  Tarefas são executadas de forma assíncrona, em paralelo com a inicialização de saudação da função hello. Olá a principal diferença entre um **primeiro plano** e um **em segundo plano** tarefa é que um **primeiro plano** tarefa impede que a função de saudação do reciclado ou desligado até que a tarefa de saudação tem terminou. Olá **em segundo plano** tarefas não têm essa restrição.

## <a name="environment-variables"></a>Variáveis de ambiente
Variáveis de ambiente são uma tarefa de inicialização do modo toopass informações tooa. Por exemplo, você pode colocar blob Olá de tooa de caminho que contém um tooinstall de programa, ou números de porta que usará a função ou recursos de toocontrol de configurações de sua tarefa de inicialização.

Há dois tipos de variáveis de ambiente para tarefas de inicialização. variáveis de ambiente estáticos e variáveis de ambiente com base nos membros de saudação [ RoleEnvironment] classe. Ambos são Olá [ambiente] seção Olá [servicedefinition. Csdef] arquivo e ambos Olá use [variável] elemento e **nome** atributo.

Saudação de usa de variáveis de ambiente estático **valor** atributo de saudação [variável] elemento. exemplo Hello acima cria a variável de ambiente Olá **MyVersionNumber** que tem um valor estático de "**1.0.0.0**". Outro exemplo seria toocreate um **StagingOrProduction** variável de ambiente que você pode definir manualmente toovalues de "**preparo**"ou"**produção**" tooperform ações diferentes de inicialização com base no valor Olá Olá **StagingOrProduction** variável de ambiente.

Variáveis de ambiente com base nos membros de saudação classe RoleEnvironment não usam Olá **valor** atributo de saudação [variável] elemento. Em vez disso, Olá [RoleInstanceValue] elemento filho, com hello apropriado **XPath** valor do atributo, é usada toocreate uma variável de ambiente com base em um membro específico de saudação [ RoleEnvironment] classe. Valores para Olá **XPath** atributo tooaccess vários [ RoleEnvironment] valores podem ser encontrados [aqui](cloud-services-role-config-xpath.md).

Toocreate por exemplo, uma variável de ambiente é "**true**" quando a instância de saudação está em execução no emulador de computação Olá, e "**false**" ao executar em nuvem Olá, use o seguinte Olá [variável] e [RoleInstanceValue] elementos:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Próximas etapas
Saiba como tooperform alguns [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md) com seu serviço de nuvem.

[Empacote](cloud-services-model-and-package.md) seu Serviço de Nuvem.  

[servicedefinition. Csdef]: cloud-services-model-and-package.md#csdef
[tarefa]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[inicialização]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[tempo de execução]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variável]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
