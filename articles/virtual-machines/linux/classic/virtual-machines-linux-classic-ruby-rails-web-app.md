---
title: aaaHost um Ruby no site de trilhos em uma VM do Linux | Microsoft Docs
description: "Configurar e hospedar um site da Web baseado no Ruby on Rails no Azure usando uma máquina virtual do Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Aplicativo Web Ruby on Rails Web em uma VM do Azure
Este tutorial mostra como toohost um Ruby no site de trilhos no Azure usando uma máquina virtual Linux.  

Este tutorial foi validado usando o Ubuntu Server 14.04 LTS. Se você usar uma distribuição de Linux diferente, talvez seja necessário toomodify Olá etapas tooinstall trilhos.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.
>
>

## <a name="create-an-azure-vm"></a>Criar uma VM do Azure
Comece criando uma VM do Azure com uma imagem do Linux.

toocreate Olá VM, você pode usar Olá portal do Azure ou hello Azure Interface de linha de comando (CLI).

### <a name="azure-portal"></a>Portal do Azure
1. O logon no hello [portal do Azure](https://portal.azure.com)
2. Clique em **novo**, em seguida, digite "Servidor do Ubuntu 14.04" na caixa de pesquisa de saudação. Clique em entrada hello retornada pela pesquisa de saudação. Para o modelo de implantação hello, selecione **clássico**, em seguida, clique em "Criar".
3. Na folha de Noções básicas de Olá, forneça valores para campos de saudação necessária: nome (para Olá VM), nome de usuário, tipo de autenticação e credenciais correspondentes do hello, assinatura do Azure, grupo de recursos e local.

   ![Criar uma nova imagem Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Depois que Olá VM for provisionada, clique no nome da VM hello e clique em **pontos de extremidade** em Olá **configurações** categoria. Localizar o ponto de extremidade SSH de hello, listado na **autônomo**.

   ![Ponto de extremidade padrão](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>CLI do Azure
Siga as etapas de saudação em [criar uma máquina Virtual executando o Linux][vm-instructions].

Depois Olá VM for provisionada, você pode obter o ponto de extremidade SSH Olá executando o comando a seguir de saudação:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Instalar o Ruby on Rails
1. Use SSH tooconnect toohello VM.
2. Da sessão SSH hello, use Olá seguindo comandos tooinstall Ruby na Olá VM:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    instalação de saudação pode levar alguns minutos. Quando for concluído, use Olá após o comando tooverify que Ruby está instalado:

        ruby -v

3. Comando a seguir de saudação do uso trilhos tooinstall:

        sudo gem install rails --no-rdoc --no-ri -V

    Use hello – não rdoc e --não ri sinalizadores tooskip instalando a documentação da saudação, que é mais rápida.
    Este comando provavelmente levará um longo tempo tooexecute, para adicionar Olá -V exibirá informações sobre o progresso da instalação hello.

## <a name="create-and-run-an-app"></a>Criar e executar um aplicativo
Ainda conectado via SSH, execute Olá comandos a seguir:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Olá [novo](http://guides.rubyonrails.org/command_line.html#rails-new) comando cria um novo aplicativo Rails. Olá [server](http://guides.rubyonrails.org/command_line.html#rails-server) inicia Olá servidor web WEBrick que acompanha os trilhos de comando. (Para uso em produção, talvez seja conveniente toouse um servidor diferente, como unicórnio ou passageiro.)

Você deve ver o seguinte de toohello semelhante de saída.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Adicionar um ponto de extremidade
1. Vá toohello [portal do Azure] [https://portal.azure.com] e selecione sua VM.

2. Selecione **pontos de EXTREMIDADE** em Olá **configurações** ao longo da página de saudação do hello borda esquerda.

3. Clique em **adicionar** na parte superior de saudação da página de saudação.

4. Em Olá **Adicionar ponto de extremidade** caixa de diálogo, insira Olá informações a seguir:

   * **Nome**: HTTP
   * **Protocolo**: TCP
   * **Porta pública**: 80
   * **Porta privada**: 3000
   * **Endereço PI flutuante**: Desabilitado
   * **Lista de controle de acesso - ordem**: 1001, ou outro valor que define a prioridade Olá desta regra de acesso.
   * **Lista de controle de acesso - Nome**: allowHTTP
   * **Lista de controle de acesso - Ação**: permitir
   * **Lista de controle de acesso - Sub-rede remota**: 1.0.0.0/16

     Esse ponto de extremidade tem uma porta pública 80 que irá rotear tráfego toohello porta privada 3000, onde o servidor de trilhos de saudação está escutando. regra de lista de controle de acesso de saudação permite tráfego público na porta 80.

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Clique em toosave Okey Olá endpoint.

6. Uma mensagem deverá aparecer indicando **Salvando o ponto de extremidade da máquina virtual**. Depois que essa mensagem desaparecerá, ponto de extremidade hello está ativo. Agora você pode testar seu aplicativo navegando toohello nome DNS de sua máquina virtual. site de saudação deve aparecer a seguir toohello semelhante:

    ![página padrão de rails][default-rails-cloud]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você já fez a maioria das etapas de saudação manualmente. Em um ambiente de produção, você deve gravar seu aplicativo em um computador de desenvolvimento e implantá-lo toohello VM do Azure. Além disso, a maioria dos ambientes de produção hospedam o aplicativo de trilhos de saudação em conjunto com outro processo de servidor, como Apache ou NginX, que trata solicitações roteamento instâncias de toomultiple do aplicativo de trilhos hello e atendendo a recursos estáticos. Para obter mais informações, consulte http://rubyonrails.org/deploy/.

toolearn mais sobre Ruby trilhos, visite Olá [Ruby trilhos guias][rails-guides].

serviços do Azure de toouse do seu aplicativo Ruby, consulte:

* [Armazenar dados desestruturados usando blobs][blobs]
* [Armazenar pares de chave/valor usando tabelas][tables]
* [Atender ao conteúdo de alta largura de banda com hello rede de fornecimento de conteúdo][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
