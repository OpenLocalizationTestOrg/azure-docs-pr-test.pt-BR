---
title: aaaCreate um pipeline de CI/CD no Azure com o Team Services | Microsoft Docs
description: "Saiba como pipeline de toocreate Visual Studio Team Services para integração contínua e entrega que implanta um tooIIS de aplicativo web em uma VM do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>Criar um pipeline de integração contínua com o Visual Studio Team Services e o IIS
compilação de saudação tooautomate, teste e as fases de implantação de desenvolvimento de aplicativos, você pode usar uma integração contínua e pipeline de implantação (CI/CD). Neste tutorial, você cria um pipeline de CI/CD usando o Visual Studio Team Services e uma VM (máquina virtual) do Windows no Azure que executa o IIS. Você aprenderá como:

> [!div class="checklist"]
> * Publicar um projeto do Team Services do tooa de aplicativo da web ASP.NET
> * Criar uma definição de build disparada por confirmações de código
> * Instalar e configurar o IIS em uma máquina virtual no Azure
> * Adicionar grupo de implantação Olá IIS instância tooa no Team Services
> * Criar uma versão de definição toopublish nova web implantar pacotes tooIIS
> * Pipeline de CI/CD de saudação do teste

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar `Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).


## <a name="create-project-in-team-services"></a>Criar o projeto no Team Services
O Visual Studio Team Services facilita a colaboração e o desenvolvimento sem manter uma solução de gerenciamento de código local. O Team Services oferece compilação, código de testes e Application Insights. Você pode escolher um repositório de controle de versão e o IDE que melhor se adapta a seu desenvolvimento de código. Para este tutorial, você pode usar uma conta gratuita toocreate um aplicativo de web ASP.NET básico e pipeline de CI/CD. Se você ainda não tem uma conta do Team Services, [crie uma](http://go.microsoft.com/fwlink/?LinkId=307137).

processo de confirmação de código do toomanage hello, criar definições e definições de versão, crie um projeto no Team Services da seguinte maneira:

1. Abra o painel Team Services em um navegador da Web e escolha **Novo projeto**.
2. Digite *myWebApp* para Olá **nome do projeto**. Deixe todos os outros toouse de valores padrão *Git* controle de versão e *Agile* processo de item de trabalho.
3. Escolha a opção de saudação muito**compartilhar com** *membros da equipe*, em seguida, selecione **criar**.
5. Quando o projeto tiver sido criado, escolha a opção de saudação muito**inicializar com um arquivo Leiame ou gitignore**, em seguida, **inicializar**.
6. Dentro de seu novo projeto, escolha **painéis** na parte superior do hello, em seguida, selecione **aberto no Visual Studio**.


## <a name="create-aspnet-web-application"></a>Criar aplicativo Web ASP.NET
Na etapa anterior do hello, você criou um projeto no Team Services. etapa final Olá abre seu novo projeto no Visual Studio. Gerenciar as confirmações de código em Olá **Team Explorer** janela. Crie uma cópia local do novo projeto e crie um aplicativo Web ASP.NET de um modelo da seguinte maneira:

1. Selecione **Clone** toocreate um repositório git local do projeto do Team Services.
    
    ![Clonar o repositório do projeto do Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. Em **Soluções**, selecione **Novo**.

    ![Criar a solução do aplicativo Web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. Selecione **Web** modelos e, em seguida, escolha Olá **aplicativo Web ASP.NET** modelo.
    1. Insira um nome para seu aplicativo, como *myWebApp*e desmarque a caixa de saudação **criar diretório para solução**.
    2. Se a opção Olá estiver disponível, desmarque caixa Olá muito**tooproject adicionar Application Insights**. Application Insights requer que você tooauthorize seu aplicativo web com o Azure Application Insights. tookeep-simples neste tutorial, ignore esse processo.
    3. Selecione **OK**.
4. Escolha **MVC** da lista de modelos de saudação.
    1. Selecione **Alterar Autenticação**, escolha **Sem Autenticação** e selecione **OK**.
    2. Selecione **Okey** toocreate sua solução.
5. Em Olá **Team Explorer** janela, escolha **alterações**.

    ![Confirmar o repositório do git alterações locais tooTeam serviços](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. Na caixa de texto de confirmação de hello, insira uma mensagem como *confirmação inicial*. Escolha **confirmar todas as e sincronização** do menu suspenso de saudação.


## <a name="create-build-definition"></a>Criar definição de build
No Team Services, você deve usar um toooutline de definição de compilação como seu aplicativo deve ser criado. Neste tutorial, podemos criar uma definição básica que usa nosso código-fonte, cria a solução hello, em seguida, criará web implanta pacote usamos toorun Olá web aplicativo em um servidor IIS.

1. No seu projeto do Team Services, escolha **Build e versão** na parte superior do hello, em seguida, selecione **cria**.
3. Selecione **+ Nova definição**.
4. Escolha Olá **ASP.NET (visualização)** modelo e selecione **aplicar**.
5. Mantenha o padrão de saudação todos os valores da tarefa. Em **obter fontes**, certifique-se de que Olá *myWebApp* repositório e *mestre* ramificação são selecionados.

    ![Criar definição de build no projeto do Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. Em Olá **gatilhos** guia, mova o controle deslizante de saudação de **habilitar esse gatilho** muito*habilitado*.
7. Salvar uma nova compilação de fila e definição de compilação Olá selecionando **Salvar & fila** , em seguida, **Salvar & fila** novamente. Mantenha os padrões de saudação e selecione **fila**.

Inspecionar como compilação hello está agendada em um agente de host, em seguida, começa toobuild. saudação de saída é similar toohello exemplo a seguir:

![Compilação bem-sucedida do projeto do Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Criar máquina virtual
tooprovide toorun uma plataforma seu aplicativo web ASP.NET, você precisa de uma máquina virtual do Windows que executa o IIS. Team Services usa toointeract um agente com a instância do IIS Olá conforme você confirmar que o código e compilações são disparadas.

Criar uma VM do Windows Server 2016 usando [este exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json). Ele leva alguns minutos para Olá script toorun e criar hello VM. Quando Olá VM tiver sido criado, abra a porta 80 para tráfego da web com [AzureRmNetworkSecurityRuleConfig adicionar](/powershell/module/azurerm.resources/new-azurermresourcegroup) da seguinte maneira:

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM, obter o endereço IP público de saudação com [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) da seguinte maneira:

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

Crie uma sessão de área de trabalho remota de tooyour VM:

```cmd
mstsc /v:<publicIpAddress>
```

No hello VM, abra um **do PowerShell do administrador** prompt de comando. Instale o IIS e os recursos necessários do .NET da seguinte maneira:

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>Criar grupo de implantação
toopush out Olá web implantar servidor IIS do pacote toohello, definir um grupo de implantação no Team Services. Este grupo permite que você toospecify quais servidores são alvo de saudação de novas compilações como confirmar tooTeam código compilações e serviços são concluídas.

1. No Team Services, escolha **Compilação e Versão** e selecione **Grupos de implantação**.
2. Escolha **Adicionar Grupo de implantação**.
3. Insira um nome para o grupo de saudação, como *myIIS*, em seguida, selecione **criar**.
4. Em Olá **registrar máquinas** seção, certifique-se de *Windows* for selecionado, marque a caixa de saudação muito**usar um token de acesso pessoal no script hello para autenticação**.
5. Selecione **copiar script tooclipboard**.


### <a name="add-iis-vm-toohello-deployment-group"></a>Adicionar grupo de implantação do IIS VM toohello
Com o grupo de implantação Olá criado, adicione cada grupo de toohello de instância do IIS. Serviços de equipe gera um script que baixa e configura um agente em Olá VM que recebe nova web implantar pacotes, em seguida, aplica tooIIS.

1. Em Olá **do PowerShell do administrador** sessão na sua VM, cole e execute o script hello copiado do Team Services.
2. Quando marcas tooconfigure solicitadas para agente hello, escolha *Y* e digite *web*.
3. Quando solicitado para a conta de usuário hello, pressione *retornar* tooaccept Olá padrões.
4. Aguarde Olá script toofinish com uma mensagem *vstsagent.account.computername de serviço foi iniciado com êxito*.
5. Em Olá **grupos de implantação** página de saudação **Build e versão** menu, abra Olá *myIIS* o grupo de implantação. Em Olá **máquinas** , verifique se que a VM está listada.

    ![VM adicionado com êxito o grupo de implantação de serviços tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>Criar definição de versão
toopublish suas compilações, criar uma definição de versão no Team Services. Essa definição é disparada automaticamente pela compilação bem-sucedida do seu aplicativo. Você escolha Olá toopush de grupo de implantação web implantar o pacote e define configurações de IIS apropriadas hello.

1. Escolha **Compilação e Versão** e selecione **Builds**. Escolha a definição de compilação Olá criada na etapa anterior.
2. Em **concluído recentemente**, escolha a compilação mais recente do hello e selecione **versão**.
3. Escolha **Sim** toocreate uma definição de versão.
4. Escolha Olá **vazio** modelo, selecione **próximo**.
5. Verifique se a definição de compilação de projeto e origem Olá são preenchidas com seu projeto.
6. Selecione Olá **implantação contínua** caixa de seleção e, em seguida, selecione **criar**.
7. Selecione caixa de lista suspensa de saudação Avançar muito**+ adicionar tarefas** e escolha *adicionar um grupo de fase de implantação*.
    
    ![Adicionar definição de toorelease de tarefa no Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. Escolha **adicionar** Avançar muito**Deploy(Preview) de aplicativo Web IIS**, em seguida, selecione **fechar**.
9. Selecione Olá **executado no grupo de implantação** tarefa pai.
    1. Para **o grupo de implantação**, selecione implantação Olá grupo criado anteriormente, como *myIIS*.
    2. Em Olá **máquina marcas** caixa, selecione **adicionar** e escolha Olá *web* marca.
    
    ![Tarefa de grupo de implantação da definição de versão para o IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. Selecione Olá **implantar: implantar o aplicativo Web IIS** tarefa tooconfigure o IIS instância configurações da seguinte maneira:
    1. Em **nome do site**, digite *Site Padrão*.
    2. Deixe Olá todas as outras configurações padrão.
12. Escolha **Salvar** e selecione **OK** duas vezes.


## <a name="create-a-release-and-publish"></a>Criar uma versão e publicar
Agora você pode enviar seu pacote de implantação Web como uma nova versão. Esta etapa se comunica com o agente de saudação em cada instância que faz parte do grupo de implantação de hello, envia Olá web implantar o pacote, em seguida, configura o aplicativo web do IIS toorun Olá atualizado.

1. Em sua definição de versão, selecione **+ Versão** e escolha **Criar Versão**.
2. Verificar se a compilação mais recente do hello está selecionada na lista suspensa de hello, juntamente com **implantação automatizada: após a criação de versão**. Selecione **Criar**.
3. Uma pequena faixa aparece na parte superior de saudação da sua definição de versão, como *versão 'Versão 1' foi criado*. Selecione Olá versão link.
4. Olá abrir **Logs** guia progresso da versão toowatch hello.
    
    ![Versão do Team Services bem-sucedida e envio do pacote de implantação Web por push](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Após a conclusão da versão de hello, abra um navegador da web e digite Olá IIP endereço público sua VM. Seu aplicativo Web ASP.NET está em execução.

    ![Aplicativo Web ASP.NET em execução na VM do IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>Testar Olá todo CI/CD pipeline
Com o aplicativo web em execução no IIS, tente pipeline de CI/CD inteiro hello. Depois que você fizer uma alteração no Visual Studio e seu código, uma compilação é disparado de confirmação que dispara uma versão da web atualizado implante pacote tooIIS:

1. No Visual Studio, abra Olá **Solution Explorer** janela.
2. Navegue tooand abrir *myWebApp | Modos de exibição | Página inicial | Cshtml*
3. Edite a linha 6 tooread:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. Salve o arquivo hello.
5. Olá abrir **Team Explorer** janela, selecione Olá *myWebApp* do projeto e escolha **alterações**.
6. Insira uma mensagem de confirmação, como *pipeline teste CI/CD*, em seguida, escolha **confirmar todos e sincronização** do menu suspenso de saudação.
7. No espaço de trabalho do Team Services, uma nova compilação é disparada de confirmação de código hello. 
    - Escolha **Compilação e Versão** e selecione **Builds**. 
    - Escolha sua definição de compilação e selecione Olá **na fila & execução** toowatch de compilação como Olá compilar progride.
9. Depois que a compilação de saudação for bem-sucedida, uma nova versão é disparada.
    - Escolha **Build e versão**, em seguida, **versões** toosee Olá web implantar pacote enviado tooyour IIS VM. 
    - Selecione Olá **atualização** status de saudação do ícone tooupdate. Olá quando *ambientes* coluna mostra uma marca de seleção verde, versão Olá foi implantada com êxito tooIIS.
11. toosee suas alterações aplicadas, atualize seu site do IIS em um navegador.

    ![Aplicativo Web ASP.NET em execução na VM do IIS pelo pipeline de CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um aplicativo web ASP.NET no Team Services e configurado build e versão definições toodeploy nova implantação da web tooIIS de pacotes em cada confirmação de código. Você aprendeu como:

> [!div class="checklist"]
> * Publicar um projeto do Team Services do tooa de aplicativo da web ASP.NET
> * Criar uma definição de build disparada por confirmações de código
> * Instalar e configurar o IIS em uma máquina virtual no Azure
> * Adicionar grupo de implantação Olá IIS instância tooa no Team Services
> * Criar uma versão de definição toopublish nova web implantar pacotes tooIIS
> * Pipeline de CI/CD de saudação do teste

Avançar toolearn tutorial do próximo toohello como toosecure um servidor web com certificados SSL.

> [!div class="nextstepaction"]
> [Proteger servidor Web com SSL](tutorial-secure-web-server.md)