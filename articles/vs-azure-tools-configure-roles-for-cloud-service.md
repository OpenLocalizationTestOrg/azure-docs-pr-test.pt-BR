---
title: "funções de saudação aaaConfigure para um Azure serviço com o Visual Studio em nuvem | Microsoft Docs"
description: "Saiba como tooset e configurar funções para serviços de nuvem do Azure usando o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Configurar funções de serviço de nuvem do Azure com o Visual Studio
Um serviço de nuvem do Azure pode ter uma ou mais funções web ou de trabalho. Para cada função, você precisa toodefine como essa função é configurada e também configurar como essa função é executado. toolearn mais informações sobre funções em serviços de nuvem, consulte o vídeo Olá [tooAzure Introdução serviços de nuvem](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

informações de saudação para seu serviço de nuvem são armazenadas no hello seguintes arquivos:

- **Servicedefinition. Csdef** -arquivo de definição de serviço Olá define configurações de tempo de execução de saudação para seu serviço de nuvem, incluindo as funções que são necessárias, os pontos de extremidade e tamanho da máquina virtual. Nenhum dos dados Olá armazenados em `ServiceDefinition.csdef` pode ser alterado quando a função está em execução.
- **ServiceConfiguration. cscfg** - arquivo de configuração de serviço Olá configura quantas instâncias de uma função são executadas e valores hello configurações de saudação definidos para uma função. Olá dados armazenados em `ServiceConfiguration.cscfg` pode ser alterado enquanto a função está em execução.

toostore diferente valores para configurações de saudação que controlam como uma função é executada, você pode definir várias configurações de serviço. Você pode usar uma configuração de serviço diferente para cada ambiente de implantação. Por exemplo, você pode definir o emulador de armazenamento do Azure local armazenamento conta conexão cadeia de caracteres toouse Olá em uma configuração de serviço local e criar outro toouse de configuração do serviço armazenamento do Azure na nuvem hello.

Quando você cria um serviço de nuvem do Azure no Visual Studio, duas configurações de serviço são criadas automaticamente e adicionado tooyour projeto do Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Configurar um serviço de nuvem do Azure
Você pode configurar um serviço de nuvem do Azure no Gerenciador de soluções no Visual Studio, conforme mostrado no hello etapas a seguir:

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.
   
    ![Menu de contexto do projeto do Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Na página de propriedades do projeto hello, selecione Olá **desenvolvimento** guia. 

    ![Página de propriedades do projeto — guia Desenvolvimento](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. Em Olá **configuração do serviço** lista, o nome de saudação select da configuração de serviço Olá que você deseja tooedit. (Se você desejar toomake altera configurações de serviço tooall Olá para esta função, selecione **todas as configurações**.)
   
    > [!IMPORTANT]
    > Se você escolher uma configuração de serviço específica, algumas propriedades ficarão desabilitadas porque elas só podem ser definidas para todas as configurações. tooedit essas propriedades, você deve selecionar **todas as configurações de**.
    > 
    > 
   
    ![Lista Configuração de Serviço para um serviço de nuvem do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Saudação de alterar número de instâncias de função
desempenho de saudação do tooimprove de seu serviço de nuvem, você pode alterar o número de saudação de instâncias de uma função em execução, com base no número de saudação de usuários ou carga Olá esperado para uma função específica. Uma outra máquina virtual é criada para cada instância de uma função quando o serviço de nuvem Olá é executado no Azure. Isso afeta a cobrança Olá para implantação de saudação deste serviço de nuvem. Para obter mais informações sobre a fatura, veja [Entenda sua fatura do Microsoft Azure](billing/billing-understand-your-bill.md).

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto hello. Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione Olá **configuração** guia.

    ![Guia Configuração](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.
   
    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. Em Olá **a contagem de instâncias** texto, digite o número de saudação de instâncias que você deseja toostart para essa função. Cada instância é executada em uma máquina virtual separada quando você publica Olá tooAzure de serviço de nuvem.

    ![Atualizando Olá contagem de instâncias](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. De saudação Visual Studio, ferramentas, selecione **salvar**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Gerenciar cadeias de conexão para contas de armazenamento
Você pode adicionar, remover ou modificar cadeias de conexão para suas configurações de serviço. Por exemplo, você pode querer uma cadeia de conexão local para uma configuração de serviço local que tem um valor de `UseDevelopmentStorage=true`. Você também poderá tooconfigure uma configuração de serviço de nuvem que usa uma conta de armazenamento no Azure.

> [!WARNING]
> Quando você insere informações chave de conta do armazenamento do Azure de Olá para uma cadeia de conexão da conta de armazenamento, essas informações são armazenadas localmente no arquivo de configuração do serviço de saudação. No entanto, atualmente essas informações não são armazenadas como texto criptografado.
> 
> 

Usando um valor diferente para cada configuração de serviço, você não tem cadeias de caracteres de conexão diferentes toouse em seu serviço de nuvem ou modificar seu código, quando você publica seu tooAzure de serviço de nuvem. Você pode usar o hello mesmo nome para a cadeia de caracteres de conexão de saudação em seu valor de código e hello é diferente, com base na configuração de serviço Olá selecionado quando você compila seu serviço de nuvem ou quando você publicá-la.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto hello. Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione Olá **configurações** guia.

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.

    ![Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd uma cadeia de caracteres de conexão, selecione **Adicionar configuração**.

    ![Adicionar cadeia de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Depois que a nova configuração de saudação adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.

    ![Nova cadeia de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -insira Olá nome que você deseja toouse para cadeia de caracteres de conexão de saudação.
    - **Tipo** - selecione **cadeia de caracteres de Conexão** da lista suspensa de saudação.
    - **Valor** -você pode inserir cadeia de caracteres de conexão Olá diretamente em Olá **valor** célula ou selecione Olá toowork de reticências (...) no hello **criar cadeia de Conexão de armazenamento** caixa de diálogo.  

1. Em Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo, selecione uma opção para **se conectar usando**. Siga as instruções de saudação para opção Olá selecionada:

    - **Emulador de armazenamento do Microsoft Azure** -se você selecionar essa opção, configurações de saudação restantes na caixa de diálogo de saudação estão desabilitadas porque se aplicam somente tooAzure. Selecione **OK**.
    - **Sua assinatura** : se você selecionar essa opção, use Olá suspensa lista tooeither, selecione e logon em uma conta da Microsoft, ou adicionar uma conta da Microsoft. Selecione uma assinatura do Azure e a conta de armazenamento. Selecione **OK**.
    - **Credenciais inseridas manualmente** - insira o nome de conta de armazenamento hello e o hello chave primária ou segundo. Selecione uma opção para **Conexão** (HTTPS é recomendado na maioria dos cenários). Selecione **OK**.

1. toodelete uma cadeia de caracteres de conexão, selecione a cadeia de caracteres de conexão hello e, em seguida, selecione **remover configuração**.

1. De saudação Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-access-a-connection-string"></a>Acessar uma cadeia de conexão de modo programático

Olá etapas a seguir mostram como tooprogrammatically acessar uma cadeia de caracteres de conexão usando o c#.

1. Adicione o seguinte Olá usando diretivas tooa c# arquivo onde você vai toouse configuração de saudação:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Olá, código a seguir ilustra um exemplo de como tooaccess uma cadeia de caracteres de conexão. Substituir saudação &lt;ConnectionStringName > espaço reservado com o valor apropriado de saudação. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Adicionar configurações personalizadas toouse em seu serviço de nuvem do Azure
As configurações personalizadas no arquivo de configuração de serviço Olá permitem adicionar um nome e valor para uma cadeia de caracteres para uma configuração de serviço específico. Você pode escolher toouse tooconfigure essa configuração que um recurso em seu serviço de nuvem lendo valor Olá Olá definindo e usando essa lógica de saudação do valor toocontrol no seu código. Você pode alterar esses valores de configuração de serviço sem ter que toorebuild seu pacote de serviço ou quando o serviço de nuvem está em execução. Seu código pode verificar se há notificações de quando uma configuração é alterada. Consulte [Evento RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Você pode adicionar, remover ou modificar configurações personalizadas para suas configurações de serviço. Talvez você queira valores diferentes para essas cadeias de caracteres para configurações de serviço diferentes.

Usando um valor diferente para cada configuração de serviço, você não tiver toouse cadeias de caracteres diferentes em seu serviço de nuvem ou modificar seu código, quando você publica seu tooAzure de serviço de nuvem. Você pode usar o hello mesmo nome para a cadeia de caracteres de saudação em seu valor de código e hello é diferente, com base na configuração de serviço Olá selecionado quando você compila seu serviço de nuvem ou quando você publicá-la.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto hello. Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione Olá **configurações** guia.

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.

    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd uma configuração personalizada, selecione **Adicionar configuração**.

    ![Adicionar configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Depois que a nova configuração de saudação adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.

    ![Nova configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -insira Olá nome da configuração de saudação.
    - **Tipo** - selecione **cadeia de caracteres** da lista suspensa de saudação.
    - **Valor** -insira Olá valor de configuração de saudação. Você pode digitar o valor de saudação diretamente em Olá **valor** célula ou selecione Olá reticências (...) tooenter Olá valor em Olá **Editar cadeia de caracteres** caixa de diálogo.  

1. toodelete uma configuração personalizada, selecione configuração de saudação e, em seguida, selecione **remover configuração**.

1. De saudação Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-access-a-custom-settings-value"></a>Acessar o valor de uma configuração personalizada de modo programático
 
Olá etapas a seguir mostram como tooprogrammatically acessar uma configuração personalizada usando c#.

1. Adicione o seguinte Olá usando diretivas tooa c# arquivo onde você vai toouse configuração de saudação:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Olá, código a seguir ilustra um exemplo de como tooaccess uma configuração personalizada. Substituir saudação &lt;SettingName > espaço reservado com o valor apropriado de saudação. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Gerenciar o armazenamento local para cada instância de função
Você pode adicionar o armazenamento do sistema de arquivos local para cada instância de uma função. Olá dados armazenados no armazenamento não está acessível por outras instâncias de função Olá para qual Olá dados são armazenados, ou por outras funções.  

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Em **Solution Explorer**, expanda o nó do projeto hello. Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione Olá **armazenamento Local** guia.

    ![Guia Armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. Em Olá **configuração do serviço** lista, verifique se **todas as configurações de** está selecionado como configurações de armazenamento local Olá aplicam configurações de serviço tooall. Qualquer outro valor resulta em todos os campos de entrada hello na página hello está sendo desativado. 

    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. tooadd uma entrada de armazenamento local, selecione **adicionar armazenamento Local**.

    ![Adicionar armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Depois que a nova entrada de armazenamento local Olá adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.

    ![Nova entrada de armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nome** -insira Olá nome que você deseja toouse para armazenamento local do novo hello.
    - **Tamanho (MB)** -insira o tamanho de saudação em MB que é necessário para o armazenamento local do novo hello.
    - **Limpeza na reciclagem da função** -selecione dados opção tooremove Olá no armazenamento local do novo hello quando a máquina virtual de saudação para função hello é reciclada.

1. toodelete uma entrada de armazenamento local, selecione entrada hello e, em seguida, selecione **remover armazenamento Local**.

1. De saudação Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-accessing-local-storage"></a>Acessar o armazenamento local de modo programático

Esta seção ilustra como tooprogrammatically acessar o armazenamento local usando c#, escrevendo um arquivo de texto de teste `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Gravar um armazenamento de toolocal do arquivo de texto

saudação de código a seguir mostra um exemplo de como o armazenamento de toolocal de arquivo toowrite um texto. Substituir saudação &lt;LocalStorageName > espaço reservado com o valor apropriado de saudação. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Localizar um arquivo gravado toolocal armazenamento

arquivo de saudação tooview criado pelo código de saudação na seção anterior do hello, siga estas etapas:
    
1.  Em Olá área de notificação do Windows, Olá ícone do Azure e, no menu de contexto hello, selecione **Mostrar UI do emulador de computação**. 

    ![Mostrar emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Selecione a função da web de saudação.

    ![Emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Em Olá **emulador de computação do Microsoft Azure** menu, selecione **ferramentas** > **abrir repositório local**.

    ![Item de menu Abrir repositório local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Quando a janela do Explorer do Windows hello for aberta, digite ' MyLocalStorageTest.txt ' em Olá **pesquisa** caixa de texto e selecione **Enter** toostart pesquisa de saudação. 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre projetos do Azure no Visual Studio, lendo [Configurando um projeto do Azure](vs-azure-tools-configuring-an-azure-project.md). Saiba mais sobre o esquema do serviço de nuvem Olá lendo [referência de esquema](https://msdn.microsoft.com/library/azure/dd179398).

