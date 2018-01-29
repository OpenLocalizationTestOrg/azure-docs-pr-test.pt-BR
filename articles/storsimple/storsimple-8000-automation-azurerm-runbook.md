---
title: "Usar o runbook de Automação do Azure para gerenciar dispositivos StorSimple | Microsoft Docs"
description: "Saiba como usar o runbook da Automação do Azure para automatizar trabalhos do StorSimple"
services: storsimple
documentationcenter: NA
author: alkohli
manager: jeconnoc
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/23/2017
ms.author: alkohli
ms.openlocfilehash: cfd0e4dbb6a4f24df5ba42cd45f9c16fbe5b493c
ms.sourcegitcommit: e6029b2994fa5ba82d0ac72b264879c3484e3dd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2017
---
# <a name="use-azure-automation-runbooks-to-manage-storsimple-devices"></a>Usar o runbook de Automação do Azure para gerenciar dispositivos StorSimple

Este artigo descreve como os runbooks da Automação do Azure são usados para gerenciar o dispositivo StorSimple 8000 Series no Portal do Azure. Há um runbook de exemplo incluído para guiá-lo pelas etapas de configuração do ambiente para executar esse runbook.


## <a name="configure-add-and-run-azure-runbook"></a>Configurar, adicionar e executar o runbook do Azure

Esta seção usa um exemplo de script do Windows PowerShell para StorSimple e fornece detalhes sobre as várias etapas necessárias para importar o script em um runbook e, em seguida, publicar e executar o runbook.

### <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você tem:

* uma assinatura ativa do Azure associada ao seu serviço de Gerenciador de Dispositivos StorSimple registrado com um dispositivo StorSimple 8000 Series.


* Windows PowerShell 5.0 instalado no computador (ou seu host Windows Server para o StorSimple se estiver usando um).


### <a name="create-automation-runbook-module-in-windows-powershell"></a>Criar o módulo de runbook de automação no Windows PowerShell

Para criar um módulo de automação para o gerenciamento de dispositivo StorSimple 8000 Series, execute as seguintes etapas:

1. Inicialize o Windows PowerShell. Crie uma nova pasta e altere o diretório para a nova pasta.

    ```
        mkdir C:\scripts\StorSimpleSDKTools
        cd C:\scripts\StorSimpleSDKTools
    ```    
2. [Baixe a CLI do NuGet](http://www.nuget.org/downloads) na pasta criada na etapa anterior. Há várias versões do _nuget.exe_. Escolha a versão correspondente ao seu SDK. Cada link de download aponta diretamente para um arquivo _.exe_. Clique com o botão direito e salve o arquivo em seu computador, em vez de executá-lo no navegador.

    Você também pode executar o comando a seguir para baixar e armazenar o script na mesma pasta que você criou anteriormente.
    
    ```
        wget https://dist.nuget.org/win-x86-commandline/latest/nuget.exe -Out C:\scripts\StorSimpleSDKTools\nuget.exe
    ```
3. Baixe o SDK dependente.

    ```
        C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.Azure.Management.Storsimple8000series
        C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.3
        C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.2.9-preview
    ```    
4. Baixe o script do projeto de exemplo do GitHub.

    ```
        wget https://raw.githubusercontent.com/anoobbacker/storsimpledevicemgmttools/master/Monitor-Backups.ps1 -Out Monitor-Backups.ps1

    ```
5. Crie um módulo de Runbook de Automação da Automação do Azure para o gerenciamento de dispositivos StorSimple 8000 Series. Na janela do Windows PowerShell, digite os seguintes comandos:

    ```
            # set path variables
            $downloadDir = "C:\scripts\StorSimpleSDKTools"
            $moduleDir = "$downloadDir\AutomationModule\Microsoft.Azure.Management.StorSimple8000Series"

            #don't change the folder name "Microsoft.Azure.Management.StorSimple8000Series"
            mkdir "$moduleDir"
            copy "$downloadDir\Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3\lib\net45\Microsoft.IdentityModel.Clients.ActiveDirectory*.dll" $moduleDir
            copy "$downloadDir\Microsoft.Rest.ClientRuntime.Azure.3.3.7\lib\net452\Microsoft.Rest.ClientRuntime.Azure*.dll" $moduleDir
            copy "$downloadDir\Microsoft.Rest.ClientRuntime.2.3.8\lib\net452\Microsoft.Rest.ClientRuntime*.dll" $moduleDir
            copy "$downloadDir\Newtonsoft.Json.6.0.8\lib\net45\Newtonsoft.Json*.dll" $moduleDir
            copy "$downloadDir\Microsoft.Rest.ClientRuntime.Azure.Authentication.2.2.9-preview\lib\net45\Microsoft.Rest.ClientRuntime.Azure.Authentication*.dll" $moduleDir
            copy "$downloadDir\Microsoft.Azure.Management.Storsimple8000series.1.0.0\lib\net452\Microsoft.Azure.Management.Storsimple8000series*.dll" $moduleDir

            #Don't change the name of the Archive
            compress-Archive -Path "$moduleDir" -DestinationPath Microsoft.Azure.Management.StorSimple8000Series.zip

    ```

6. Verifique se um arquivo zip do módulo de automação é criado em `C:\scripts\StorSimpleSDKTools`.

    ![verify-automation-module](./media/storsimple-8000-automation-azurerm-runbook/verify-automation-module.png)

7. A saída a seguir é apresentada quando o módulo de automação é criado por meio do Windows PowerShell. 

    ```
    -----------------------------------------
    Windows PowerShell
    Copyright (C) 2016 Microsoft Corporation. All rights reserved.

    PS C:\WINDOWS\system32> mkdir C:\scripts\StorSimpleSDKTools

        Directory: C:\scripts

    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    d-----       10/18/2017   8:43 AM                StorSimpleSDKTools


    PS C:\WINDOWS\system32> cd c:\scripts\StorSimpleSDKTools
    PS C:\scripts\StorSimpleSDKTools> wget https://dist.nuget.org/win-x86-commandline/latest/nuget.exe -Out C:\scripts\StorS
    impleSDKTools\nuget.exe
    PS C:\scripts\StorSimpleSDKTools> C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.Azure.Management.Storsimple8
    000series

    -------------------------------------------
    CUT              CUT  
    -------------------------------------------
    Successfully installed 'Microsoft.Azure.Management.Storsimple8000series 1.0.0' to C:\scripts\StorSimpleSDKTools
    Executing nuget actions took 1.77 sec
    PS C:\scripts\StorSimpleSDKTools> C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.IdentityModel.Clients.Active
    Directory -Version 2.28.3

    -------------------------------------------
    CUT              CUT  
    -------------------------------------------
    Successfully installed 'Microsoft.IdentityModel.Clients.ActiveDirectory 2.28.3' to C:\scripts\StorSimpleSDKTools
    Executing nuget actions took 927.64 ms
    PS C:\scripts\StorSimpleSDKTools> C:\scripts\StorSimpleSDKTools\nuget.exe install Microsoft.Rest.ClientRuntime.Azure.Aut
    hentication -Version 2.2.9-preview

    -------------------------------------------
    CUT              CUT  
    -------------------------------------------
    Successfully installed 'Microsoft.Rest.ClientRuntime.Azure.Authentication 2.2.9-preview' to C:\scripts\StorSimpleSDKTool
    s
    Executing nuget actions took 717.48 ms
    PS C:\scripts\StorSimpleSDKTools> wget https://raw.githubusercontent.com/anoobbacker/storsimpledevicemgmttools/master/Mo
    nitor-Backups.ps1 -Out Monitor-Backups.ps1
    PS C:\scripts\StorSimpleSDKTools> # set path variables
    PS C:\scripts\StorSimpleSDKTools>             $downloadDir = "C:\scripts\StorSimpleSDKTools"
    PS C:\scripts\StorSimpleSDKTools>             $moduleDir = "$downloadDir\AutomationModule\Microsoft.Azure.Management.Sto
    rSimple8000Series"
    PS C:\scripts\StorSimpleSDKTools>
    PS C:\scripts\StorSimpleSDKTools>             #don't change the folder name "Microsoft.Azure.Management.StorSimple8000Se
    ries"
    PS C:\scripts\StorSimpleSDKTools>             mkdir "$moduleDir"

        Directory: C:\scripts\StorSimpleSDKTools\AutomationModule


    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    d-----       10/18/2017   8:48 AM                Microsoft.Azure.Management.StorSimple8000Series

    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Microsoft.IdentityModel.Clients.ActiveDirectory.2.28.3\
    lib\net45\Microsoft.IdentityModel.Clients.ActiveDirectory*.dll" $moduleDir
    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Microsoft.Rest.ClientRuntime.Azure.3.3.7\lib\net452\Mic
    rosoft.Rest.ClientRuntime.Azure*.dll" $moduleDir
    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Microsoft.Rest.ClientRuntime.2.3.8\lib\net452\Microsoft
    .Rest.ClientRuntime*.dll" $moduleDir
    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Newtonsoft.Json.6.0.8\lib\net45\Newtonsoft.Json*.dll" $
    moduleDir
    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Microsoft.Rest.ClientRuntime.Azure.Authentication.2.2.9
    -preview\lib\net45\Microsoft.Rest.ClientRuntime.Azure.Authentication*.dll" $moduleDir
    PS C:\scripts\StorSimpleSDKTools>             copy "$downloadDir\Microsoft.Azure.Management.Storsimple8000series.1.0.0\l
    ib\net452\Microsoft.Azure.Management.Storsimple8000series*.dll" $moduleDir
    PS C:\scripts\StorSimpleSDKTools>
    PS C:\scripts\StorSimpleSDKTools>             #Don't change the name of the Archive
    PS C:\scripts\StorSimpleSDKTools>             compress-Archive -Path "$moduleDir" -DestinationPath Microsoft.Azure.Manag
    ement.StorSimple8000Series.zip
    PS C:\scripts\StorSimpleSDKTools>

    -------------------------------------------

    ```

### <a name="import-publish-and-run-automation-runbook"></a>Importar, publicar e executar o runbook de automação

1. Crie uma conta de automação Executar Como do Azure no Portal do Azure. Para fazer isso, vá para **Marketplace do Azure > Tudo** e, em seguida, pesquise **Automação**. Selecione **Contas de automação**.

    ![search-automation](./media/storsimple-8000-automation-azurerm-runbook/automation1.png)

2. Na folha **Adicionar Conta de Automação**:

    1. Forneça o **Nome** da Conta de automação.
    2. Selecione a **Assinatura** vinculada para seu serviço de Gerenciador de Dispositivos StorSimple.
    3. Crie um novo grupo de recursos ou selecione um existente.
    4. Selecione uma **Localização** (se possível, a mesma em que o serviço está em execução).
    5. Deixe a opção **Criar Conta Executar Como** padrão selecionada.
    5. Opcionalmente, marque **Fixar no painel**. Clique em **Criar**.

        ![create-automation-account](./media/storsimple-8000-automation-azurerm-runbook/create-automation-account.png)

    Depois de a conta de automação ser criada com sucesso, você será notificado. Para obter mais informações sobre como criar uma Conta de Automação, vá para [Criar a conta Executar como](https://docs.microsoft.com/azure/automation/automation-create-runas-account).

3. Para garantir que a conta de automação criada possa acessar o serviço de Gerenciador de Dispositivos StorSimple, você precisa atribuir as permissões apropriadas para a conta de automação. Acesse **Controle de acesso** no serviço do Gerenciador de Dispositivos StorSimple. Clique em **+ Adicionar** e forneça o nome de sua Conta de Automação do Azure. **Salve** as configurações.

    ![add-permissions-automation-account](./media/storsimple-8000-automation-azurerm-runbook/goto-add-roles.png)

4. Na conta recém-criada, vá para **Recursos Compartilhados > Módulos** e clique em **+ Adicionar módulo**.

5. Na folha **Adicionar módulo**, navegue até o local do módulo compactado, selecione e abra o módulo. Clique em **OK**.

    ![add-module](./media/storsimple-8000-automation-azurerm-runbook/add-module.png)

6. Vá para **Automação de Processos > Runbooks e clique em + Adicionar um runbook**. Na folha **Adicionar runbook**, clique em **Importar um runbook existente**. Aponte para o arquivo de script do Windows PowerShell para o **Arquivo de Runbook**. O tipo de runbook é selecionado automaticamente. Forneça um nome e uma descrição opcional para o runbook. Clique em **Criar**.

    ![add-module](./media/storsimple-8000-automation-azurerm-runbook/import-runbook.png)

7. O runbook é adicionado à lista de runbooks. Selecione e clique neste runbook.

    ![click-new-runbook](./media/storsimple-8000-automation-azurerm-runbook/verify-runbook-created.png)

8. Edite o runbook e clique em **Painel de teste**. Forneça os parâmetros, como o nome do seu serviço de Gerenciador de Dispositivos StorSimple, o nome do dispositivo StorSimple e a assinatura. **Inicie** o teste. O relatório é gerado quando a execução é concluída. Para obter mais informações, vá para [como testar um runbook](../automation/automation-first-runbook-textual-powershell.md#step-3---test-the-runbook).

    ![test-runbook](./media/storsimple-8000-automation-azurerm-runbook/test-runbook.png)

9. Inspecione a saída do runbook no painel de teste. Se estiver satisfeito, feche o painel. Clique em **Publicar** e, quando a confirmação for solicitada, confirme e publique o runbook.

    ![publish-runbook](./media/storsimple-8000-automation-azurerm-runbook/publish-runbook.png)


## <a name="next-steps"></a>Próximas etapas

[Usar o serviço do Gerenciador de Dispositivos StorSimple para gerenciar seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).