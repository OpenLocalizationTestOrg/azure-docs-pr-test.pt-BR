---
title: "implantação da máquina virtual aaaAzure com Chef | Microsoft Docs"
description: "Saiba como toouse Chef toodo automatizado implantação da máquina virtual e a configuração no Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Automatizando a implantação de máquina virtual do Azure com o Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

O Chef é uma excelente ferramenta para a entrega de automação e configurações de estado de desejado.

Com nossa última versão de api de nuvem, Chef fornece integração perfeita com o Azure, oferecendo Olá tooprovision de capacidade e implantar os estados de configuração por meio de um único comando.

Neste artigo, mostrarei como tooset o seu ambiente de Chef tooprovision virtuais do Azure máquinas e orientá-lo a criar uma política ou um "Livro de receitas" e, em seguida, implantar este tooan livro de receitas máquina virtual do Azure.

Vamos começar!

## <a name="chef-basics"></a>Noções básicas do Chef
Antes de começar, sugerimos que você revisar os conceitos básicos de saudação do Chef. Há um excelente material <a href="http://www.chef.io/chef" target="_blank">aqui</a> e recomendo que você leia rapidamente antes de tentar este passo-a-passo. No entanto, será recapitular Noções básicas de saudação antes de começar.

Olá diagrama a seguir mostra a arquitetura chefe de alto nível hello.

![][2]

O Chef tem três componentes principais de arquitetura: Chef Server, Chef Client (nó) e Chef Workstation.

Olá servidor nosso ponto de gerenciamento e há duas opções para o servidor de saudação: uma solução hospedada ou uma solução local. Vamos usar uma solução hospedada.

Cliente do Chef Hello (nó) é agente Olá localizado nos servidores de saudação que está gerenciando.

Olá estação de trabalho do Chef é nossa estação de trabalho do administrador em que criamos nossas políticas e executar os comandos de gerenciamento. Podemos executar Olá **knife** nossa infraestrutura de comando de saudação toomanage de estação de trabalho do Chef.

Também há conceito de saudação de "Guias" e "Receitas". Esses são efetivamente políticas hello, definir e aplicar tooour servidores.

## <a name="preparing-hello-workstation"></a>Preparando a estação de trabalho Olá
Primeiro, permite que a estação de trabalho de preparação hello. Estou usando uma estação de trabalho padrão do Windows. Precisamos toocreate toostore um diretório de nossos arquivos de configuração e guias.

Primeiro, crie um diretório chamado C:\chef.

Em seguida, crie um segundo diretório chamado c:\chef\cookbooks.

Agora precisamos toodownload nosso arquivo de configurações do Azure para que chefe possa se comunicar com nossa assinatura do Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Baixe o publicar configurações usando hello PowerShell Azure [AzurePublishSettingsFile Get](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando. 

Salvar Olá publica arquivo de configurações em C:\chef.

## <a name="creating-a-managed-chef-account"></a>Criando uma conta gerenciada do Chef
Inscreva-se para uma conta hospedada do Chef [aqui](https://manage.chef.io/signup).

Durante o processo de inscrição hello, você será solicitado a toocreate uma nova organização.

![][3]

Depois de criar a sua organização, baixe Olá starter kit.

![][4]

> [!NOTE]
> Se você receber um aviso informando que as chaves serão redefinidas, é tooproceed okey como não temos nenhuma infraestrutura existente configurada ainda.
> 
> 

Este arquivo zip do kit inicial contém arquivos de configuração de organização e chaves.

## <a name="configuring-hello-chef-workstation"></a>Configurando a estação de trabalho do hello Chef
Extrai o conteúdo de saudação do hello chef starter.zip tooC:\chef.

Copie todos os arquivos em starter\chef-chef-repo\.chef tooyour c:\chef directory.

Seu diretório agora deve ser semelhante a saudação de exemplo a seguir.

![][5]

Agora você deve ter quatro arquivos, incluindo Olá arquivo de publicação do Azure na raiz de saudação do c:\chef.

arquivos PEM de saudação contenham sua organização e chaves privadas de administração para comunicação enquanto o arquivo de knife Olá contém sua configuração de ferramentas. Precisaremos de arquivo de knife tooedit hello.

Abra o arquivo de saudação em seu editor de preferência e modifique cookbook_path"hello" Removendo Olá /... / do caminho Olá para que ele apareça como mostrado a seguir.

    cookbook_path  ["#{current_dir}/cookbooks"]

Também adicione Olá linha refletindo nome hello do Azure publica o arquivo de configurações.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

O arquivo knife. RB agora deve ser semelhante toohello exemplo a seguir.

![][6]

Essas linhas garantirá que Knife faz referência a saudação guias diretório em c:\chef\cookbooks e também usa o nosso arquivo de configurações de publicação do Azure durante as operações do Azure.

## <a name="installing-hello-chef-development-kit"></a>Olá chefe Development Kit de instalação
Próxima [baixar e instalar](http://downloads.getchef.com/chef-dk/windows) Olá tooset ChefDK (chefe Development Kit) a sua estação de trabalho do Chef.

![][7]

Instale no local padrão de saudação do c:\opscode. Esta instalação levará cerca de 10 minutos.

Confirme que sua variável PATH contém entradas para C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Se eles não estão lá, certifique-se que adicionar esses caminhos!

*Observação Olá ordem de saudação caminho é importante!* Se seus caminhos opscode não estão na ordem correta hello, que você terá problemas.

Reinicie a estação de trabalho antes de continuar.

Em seguida, vamos instalar extensão do Knife Azure hello. Isso fornece ferramentas com hello "Plug-in do Azure".

Execute Olá comando a seguir.

    chef gem install knife-azure ––pre

> [!NOTE]
> argumento de pré-Olá garante que você está recebendo a última versão RC Olá de saudação Knife Azure plug-in que fornece acesso toohello último conjunto de APIs.
> 
> 

É provável que um número de dependências também será instalado no hello simultaneamente.

![][8]

tooensure que tudo está configurado corretamente, Olá executar comando a seguir.

    knife azure image list

Se tudo estiver configurado corretamente, você verá uma lista de imagens do Azure disponíveis rolar.

Parabéns. Configurar a estação de trabalho Olá!

## <a name="creating-a-cookbook"></a>Criação de um Guia
Um livro de receitas é usado pelo Chef toodefine um conjunto de comandos que você deseja tooexecute no seu cliente gerenciado. Criar um livro de receitas é simples e usamos Olá **chef gerar livro de receitas** comando toogenerate nosso modelo de livro de receitas. Eu chamarei meu servidor Web do Guia como eu faria com a política que implanta automaticamente o IIS.

Em seu diretório C:\Chef execute Olá comando a seguir.

    chef generate cookbook webserver

Isso irá gerar um conjunto de arquivos no diretório Olá C:\Chef\cookbooks\webserver. Agora precisamos de conjunto de saudação do toodefine de comandos gostaríamos que nossas tooexecute de cliente do Chef na máquina virtual gerenciada.

comandos de saudação são armazenados no RB de arquivo hello. Nesse arquivo, eu vai definir um conjunto de comandos que instala o IIS, o IIS é iniciado e copia um modelo arquivo toohello na pasta wwwroot.

Modificar o arquivo de C:\chef\cookbooks\webserver\recipes\default.rb hello e adicione Olá linhas a seguir.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Salve o arquivo de saudação quando terminar.

## <a name="creating-a-template"></a>Criando um modelo
Conforme mencionado anteriormente, é preciso toogenerate um arquivo de modelo que será usado como nossa página de Default.

Execute Olá modelo de saudação do comando toogenerate a seguir.

    chef generate template webserver Default.htm

Agora, navegar toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb arquivo. Editar arquivo hello adicionando um código de "Hello World" HTML simples e, em seguida, salve o arquivo hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Carregar Olá livro de receitas toohello Chef Server
Nesta etapa, estamos fazendo uma cópia de saudação livro de receitas que você criou na máquina local e carregá-lo toohello o servidor do Chef hospedado. Uma vez carregado, Olá livro de receitas aparecerá sob Olá **política** guia.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Implantar uma máquina virtual com o Knife Azure
Agora vamos implantar uma máquina virtual do Azure e aplicar hello "Webserver" livro de receitas que instalará nossa IIS página da web padrão e o serviço web.

Em ordem toodo isso, use Olá **knife azure server criar** comando.

Estou exemplo hello comando aparece em seguida.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

parâmetros de saudação são autoexplicativos. Substitua variáveis específicas e executar.

> [!NOTE]
> Por meio da linha de comando Olá Olá eu estou também automatizar meu regras de filtro de rede do ponto de extremidade usando o parâmetro de pontos de extremidade tcp – hello. Eu abrir portas 80 e página da web do tooprovide acesso toomy 3389 e sessão RDP.
> 
> 

Quando você executar o comando hello, vá toohello Azure portal e você verá sua máquina começar tooprovision.

![][13]

prompt de comando Olá aparece em seguida.

![][10]

Após a conclusão da implantação hello, podemos deve ser capaz de tooconnect toohello web Services pela porta 80 tinha abrir porta hello quando nós provisionamos máquina virtual Olá Olá comando Knife Azure. Como essa máquina virtual é Olá de máquina virtual somente em meu serviço de nuvem, eu o conectarei com hello url do serviço de nuvem.

![][11]

Como você pode ver, fui criativo com meu código HTML.

Não se esqueça de que nós também pode se conectar por meio de uma sessão RDP do portal do Azure através da porta 3389 de saudação.

Espero que isso tenha sido útil! Siga adiante e comece sua jornada de infraestrutura como código com o Azure hoje mesmo!

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
