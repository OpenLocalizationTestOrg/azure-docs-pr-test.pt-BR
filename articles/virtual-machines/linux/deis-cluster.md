---
title: "aaaDeploy Deis 3 nós cluster | Microsoft Docs"
description: "Este artigo descreve como toocreate 3 nós Deis cluster no Azure usando um modelo do Gerenciador de recursos do Azure"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Implantar e configurar um cluster Deis de 3 nós no Azure
Este artigo percorre o provisionamento de um cluster [Deis](http://deis.io/) no Azure. Ele abrange todas as etapas de saudação criem Olá toodeploying de certificados necessários e dimensionamento de um exemplo **vá** aplicativo no cluster recentemente provisionados hello.

Olá diagrama a seguir mostra arquitetura de saudação do sistema Olá implantado. Um administrador do sistema gerencia Olá cluster usando Deis ferramentas como **deis** e **deisctl**. As conexões são estabelecidas por meio de um balanceador de carga do Azure, que encaminha Olá conexões tooone de membro Olá nós no cluster de saudação. o acesso de clientes do Hello implantado aplicativos por meio do balanceador de carga de saudação. Nesse caso, o balanceador de carga Olá encaminha Olá tráfego tooa Deis malha do roteador, o que mais routs contêineres do Docker toocorresponding tráfego hospedados no cluster hello.

  ![Diagrama da arquitetura do cluster Deis implantado](./media/deis-cluster/architecture-overview.png)

Ordem toorun por meio de saudação etapas a seguir, você precisará:

* Uma assinatura ativa do Azure. Se você não tiver uma, é possível obter uma avaliação gratuita em [azure.com](https://azure.microsoft.com/).
* Um trabalho ou escola id toouse recursos do Azure grupos. Se você tiver uma conta pessoal e faça logon com uma id da Microsoft, será necessário muito[criar uma id de trabalho do seu personal](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* O - dependendo do seu sistema operacional de cliente - Olá [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [CLI do Azure para Mac, Linux e Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL é usado toogenerate Olá necessários certificados.
* Um cliente Git como o [Git Bash](https://git-scm.com/).
* aplicativo de exemplo hello tootest, também será necessário um servidor DNS. Você pode usar quaisquer servidores DNS ou serviços que dão suporte a registros de curinga A.
* Um computador toorun Deis ferramentas de cliente. Você pode usar um computador local ou uma máquina virtual. Você pode executar essas ferramentas em praticamente qualquer distribuição de Linux, mas instruções a seguir hello usam Ubuntu.

## <a name="provision-hello-cluster"></a>Cluster de saudação de provisão
Nesta seção, você usará um [do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modelo do repositório de código-fonte aberto Olá [modelos de início rápido do azure](https://github.com/Azure/azure-quickstart-templates). Primeiro, você copiará para o modelo de saudação. Em seguida, criará um novo par de chaves SSH para autenticação. Depois, você configurará um novo identificador para o cluster. E, finalmente, você usará o script de Shell hello ou cluster de Olá Olá PowerShell script tooprovision.

1. Repositório de saudação do clone: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Acesse a pasta do modelo de toohello:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Crie um novo par de chaves SSH usando ssh-keygen:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Gere um certificado usando Olá acima da chave privada:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Vá muito[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate um novo token de cluster, que se parece algo como:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Cada cluster CoreOS precisa toohave um token exclusivo desse serviço gratuito. Veja a [documentação do CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) para obter mais detalhes.
6. Modificar Olá **nuvem config.yaml** tooreplace Olá existente de arquivos **descoberta** token com um novo token de saudação:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Modificar Olá **azuredeploy parameters.json** arquivo: certificado Olá aberto criado na etapa 4 em um editor de texto. Copiar todo o texto entre `----BEGIN CERTIFICATE-----` e `-----END CERTIFICATE-----` em Olá **sshKeyData** parâmetro (você precisará tooremove todos os caracteres de nova linha).
8. Modificar Olá **newStorageAccountName** parâmetro. Esta é a conta de armazenamento de saudação para discos de sistema operacional da VM. Este nome de conta tem toobe globalmente exclusivo.
9. Modificar Olá **publicDomainName** parâmetro. Isso se tornará parte do nome DNS Olá associado com o IP público do balanceador de carga de saudação. Olá FQDN final terá o formato de saudação do *[valor desse parâmetro]*. *[Região]* . cloudapp.azure.com. Por exemplo, se você especificar o nome hello como deishbai32 e grupo de recursos de saudação for região Oeste dos EUA de toohello implantado, Olá final balanceador de carga do FQDN tooyour será deishbai32.westus.cloudapp.azure.com.
10. Salve o arquivo de parâmetro hello. E, em seguida, você pode provisionar o cluster hello usando o Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    ou o CLI do Azure:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Quando o grupo de recursos Olá é provisionado, você pode ver todos os recursos de saudação em grupo Olá no portal clássico do Azure. Conforme mostrado no hello seguinte captura de tela, hello grupo de recursos contém uma rede virtual com três VMs, que são unidas toohello mesmo conjunto de disponibilidade. grupo de saudação também contém um balanceador de carga, que tem um IP público associado.
    
    ![Olá provisionado o grupo de recursos no portal clássico do Azure](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Instalar o cliente Olá
Você precisa **deisctl** toocontrol sua Deis cluster. Embora deisctl é instalado automaticamente em todos os nós de cluster Olá, é um deisctl toouse de prática recomendada em um computador administrativo separado. Além disso, como todos os nós são configurados com apenas os endereços IP privados, será necessário toouse SSH túnel por meio do balanceador de carga hello, que tem um IP público, máquinas de nó toohello tooconnect. Olá, estas são as etapas de saudação de configuração de deisctl em uma máquina virtual ou Ubuntu físico separado.

1. Instale o deis deisctl:mkdir
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Adicione o agente toossh chave privada:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Configure o deisctl:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

modelo Hello define regras de NAT de entrada que mapeiam 2223 tooinstance 1, 2224 tooinstance 2 e 2225 tooinstance 3. Isso fornece redundância para usar a ferramenta de deisctl hello. Você pode examinar essas regras no portal clássico do Azure:

![Regras NAT no balanceador de carga Olá](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Atualmente o modelo Olá só dá suporte a clusters de 3 nós. Isso se deve a uma limitação na definição da regra NAT do modelo do Gerenciador de Recursos do Azure, que não dá suporte à sintaxe de loop.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Instale e inicie Olá Deis plataforma
Agora você pode usar deisctl tooinstall e iniciar Olá Deis plataforma:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Plataforma de saudação inicial leva um tempo (até 10 minutos). Especialmente, iniciando o serviço de construtor Olá pode levar muito tempo. E, às vezes, leva alguns toosucceed de tentativas: se a operação de saudação parecer toohang, tente digitar `ctrl+c` toobreak a execução do comando hello e tente novamente.
> 
> 

Você pode usar `deisctl list` tooverify se todos os serviços estão em execução:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Parabéns! Agora, você tem um cluster Deis em execução no Azure! Em seguida, vamos implantar um cluster de saudação do Go aplicativo toosee na ação de exemplo.

## <a name="deploy-and-scale-a-hello-world-application"></a>Implantar e dimensionar um aplicativo Hello World
Olá etapas a seguir mostram como toodeploy "Hello World" Vá cluster toohello de aplicativo. Olá etapas são baseadas na [Deis documentação](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Para Olá roteamento malha toowork corretamente, você precisará toohave um curinga um registro para o seu domínio apontando toohello o IP público saudação do balanceador de carga. Olá seguinte captura de tela mostra Olá um registro para um registro de domínio de exemplo em GoDaddy:
   
    ![Registro A do GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Instalar e o deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Crie uma nova chave SSH e depois adicione Olá tooGitHub de chave pública (é claro, também é possível reutilizar suas chaves existentes). toocreate um par de chaves de SSH novo, use:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Adicione id_rsa.pub ou a chave pública Olá de sua escolha, tooGitHub. Você pode fazer isso usando Olá adicionar SSH botão da chave em sua tela de configuração de chaves SSH:
   
   ![Chave do GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Registrar um novo usuário:
   
        deis register http://deis.[your domain]
   <p />
6. Adicione a chave SSH hello:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Crie um aplicativo.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.push do git Olá irão disparar Docker imagens toobe criado e implantado, que o levará alguns minutos. Na minha experiência, ocasionalmente, pode travar etapa 10 (repositório de tooprivate de imagem Pushing). Quando isso acontece, você pode interromper o processo de hello, usando o aplicativo hello remover ' deis aplicativos: destruir – um <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nome de saudação do seu aplicativo. Se tudo funcionar, você verá algo parecido com a seguinte Olá final Olá das saídas de comando:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Verifique se o aplicativo hello está funcionando:
   
        curl -S http://[your application name].[your domain]
   Você deverá ver:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Escala Olá aplicativo too3 instâncias:
    
        deis scale cmd=3
    <p />
11. Opcionalmente, você pode usar deis info tooexamine detalhes do seu aplicativo. Olá seguintes saídas são de minha implantação de aplicativo:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Próximas etapas
Este artigo analisou todos os tooprovision de etapas de saudação Deis um novo cluster no Azure usando um modelo do Gerenciador de recursos do Azure. modelo de saudação dá suporte a redundância em ferramentas de conexões, bem como o balanceamento de carga para aplicativos implantados. modelo de saudação também evita usando IPs públicos em nós de membro, que salva preciosos recursos IP públicos e fornece um ambiente mais seguro toohost aplicativos. toolearn mais, consulte Olá artigos a seguir:

[Visão Geral do Azure Resource Manager][resource-group-overview]  
[Como toouse Olá CLI do Azure][azure-command-line-tools]  
[Usando o Azure PowerShell com o Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
