---
title: "Olá aaaUsing extensão da VM Docker para Linux no Azure"
description: "Descreve o Docker e extensões de máquinas virtuais do Azure hello e mostra como tooprogrammatically criar máquinas virtuais no Azure são hosts de docker da linha de comando de saudação usando Olá CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Usando a extensão da VM Docker de saudação do hello Azure Interface de linha de comando (CLI do Azure)
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre como usar a extensão de VM Docker Olá com o modelo do Gerenciador de recursos de hello, consulte [aqui](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este tópico descreve como toocreate uma VM com Olá extensão da VM Docker do hello serviço modo de gerenciamento (asm) em CLI do Azure em qualquer plataforma. [Docker](https://www.docker.com/) é uma saudação mais populares abordagens de virtualização que usa [contêineres Linux](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como um modo de isolamento de dados e computação em recursos compartilhados. Você pode usar a extensão de VM Docker hello e hello [agente Linux do Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate uma VM Docker que hospeda qualquer número de contêineres para seus aplicativos no Azure. toosee uma discussão detalhada sobre contêineres e suas vantagens, consulte Olá [Docker alto nível de quadro](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Como toouse Olá extensão da VM Docker com o Azure
extensão de VM Docker toouse Olá com o Azure, você deve instalar uma versão de hello [Interface de linha de comando do Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI do Azure) maior do que 0.8.6 (como de saudação esta gravação atual versão 0.10.0). Você pode instalar Olá CLI do Azure no Windows, Mac e Linux.

Olá processo completo toouse Docker no Azure é simple:

* Instalar Olá CLI do Azure e suas dependências no computador de saudação do qual você deseja toocontrol do Azure (no Windows, isso será uma distribuição do Linux em execução como uma máquina virtual)
* Usar o hello Azure CLI Docker comandos toocreate um host de VM Docker no Azure
* Use Olá local Docker comandos toomanage seus contêineres de Docker em sua VM Docker no Azure.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Instalar hello Azure Interface de linha de comando (CLI do Azure)
tooinstall e configurar Olá CLI do Azure, consulte [como tooinstall Olá Interface de linha de comando do Azure](../../../cli-install-nodejs.md). instalação de saudação tooconfirm, tipo `azure` no prompt de comando do hello e após um breve momento você deve ver Olá arte ASCII de CLI do Azure, que lista Olá basic comandos tooyou disponível. Se instalação Olá funcionou corretamente, você deve ser capaz de tootype `azure help vm` e ver se um dos comandos de saudação listado é "docker".

> [!NOTE]
> Docker tem as ferramentas do Windows, [Docker máquina](https://docs.docker.com/installation/windows/), que você também pode usar a criação de um cliente do docker que você pode usar toowork com VMs do Azure como hosts de docker Olá tooautomate.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Conecte-se Olá CLI do Azure tootooyour conta do Azure
Antes de usar o hello CLI do Azure, você deve associar suas credenciais de conta do Azure com hello CLI do Azure em sua plataforma. Olá seção [como tooconnect tooyour assinatura do Azure](../../../xplat-cli-connect.md) explica como tooeither baixar e importar sua **. publishsettings** arquivo ou associar a CLI do Azure com uma id organizacional.

> [!NOTE]
> Há algumas diferenças no comportamento quando um ou hello outros métodos de autenticação, então ser se tooread Olá documento acima funcionalidade diferente do toounderstand hello.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Instalar o Docker e usar Olá extensão da VM Docker do Azure
Siga Olá [instruções de instalação do Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localmente no seu computador.

toouse Docker com uma máquina Virtual do Azure, imagem do Linux Olá usada para Olá VM deve ter Olá [agente de VM do Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) instalado. No momento, apenas dois tipos de imagens possibilitam isso:

* Uma imagem do Ubuntu de saudação Galeria de imagens do Azure ou
* Uma imagem personalizada do Linux que você criou com hello agente de VM do Linux do Azure instalado e configurado. Consulte [agente de VM do Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como toobuild uma VM do Linux personalizado com hello Azure VM Agent.

### <a name="using-hello-azure-image-gallery"></a>Usando a Galeria de imagens do Azure Olá
A partir de uma sessão de Terminal ou Bash, usar Olá comando CLI do Azure toolocate Olá imagem Ubuntu mais recente no hello VM Galeria toouse digitando a seguir

`azure vm image list | grep Ubuntu-14_04`

e selecione um dos nomes de imagem hello, como `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, e o comando a seguir do uso Olá toocreate uma nova VM usando essa imagem.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

onde:

* *&lt;nome de VM cloudservice&gt;*  é nome de saudação do hello VM que se tornará o computador de host de contêiner Olá Docker no Azure
* *&lt;nome de usuário&gt;*  é o nome de usuário de saudação do usuário de raiz de padrão de saudação do hello VM
* *&lt;senha&gt;*  é a senha Olá Olá *username* conta que atende aos padrões de saudação de complexidade do Azure

> [!NOTE]
> Atualmente, a senha deve ter pelo menos 8 caracteres, conter minúscula e maiuscula caracteres, um número e um caractere especial, como um dos seguintes caracteres de saudação: `!@#$%^&+=`. Não, o período Olá final Olá Olá anterior frase não é um caractere especial.
> 
> 

Se o comando Olá foi bem-sucedida, você verá algo parecido com hello seguinte, dependendo de argumentos preciso hello e opções que você usou:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> Criando uma máquina virtual pode levar alguns minutos, mas depois foi provisionado (valor de estado de saudação é `ReadyRole`) Olá inicia do Docker daemon (Olá serviço do Docker) e você pode conectar o host do contêiner Docker toohello.
> 
> 

Olá tootest VM Docker que você criou no Azure, o tipo

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

onde  *&lt;vm-nome-você-usado&gt;*  é Olá nome da máquina virtual Olá usado na sua chamada muito`azure vm docker create`. Você verá algo semelhante toohello seguinte, que indica que a VM do Host do Docker está ativo e em execução no Azure e aguardando seus comandos. 

Agora você pode tentar tooconnect usando suas informações de tooobtain de cliente do docker (em algumas configurações de cliente do Docker, como no Mac, talvez seja necessário toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Apenas toobe certeza de que ele é funcionar, você pode examinar hello VM para Olá extensão Docker:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Autenticação da máquina virtual host do Docker
Além disso toocreating Olá VM Docker, Olá `azure vm docker create` comando também cria automaticamente Olá certificados necessários tooallow seu host do contêiner do Azure Docker cliente computador tooconnect toohello usando HTTPS, e Olá certificados são armazenados nos dois Olá máquinas cliente e host, conforme apropriado. Nas tentativas subsequentes, certificados existentes Olá são reutilizados e compartilhados com o novo host de saudação.

Por padrão, os certificados são colocados em `~/.docker`, e o Docker será toorun configurado na porta **2376**. Se você gostaria que toouse uma porta diferente ou diretório, você pode usar um dos seguintes Olá `azure vm docker create` opções de linha de comando tooconfigure o Docker contêiner host VM toouse uma porta diferente ou certificados diferentes para conectar clientes:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

Olá daemon do Docker no host de saudação é toolisten configurado para e autenticar o cliente conexões Olá especificado usando certificados de saudação de porta gerado pelo Olá `azure vm docker create` comando. Olá cliente deve ter esses certificados toogain acessar toohello Docker host.

> [!NOTE]
> Um host de rede em execução sem esses certificados serão tooanyone vulnerável que pode tooconnect toohello máquina. Antes de modificar a configuração padrão de saudação, certifique-se de que entendeu Olá riscos tooyour computadores e aplicativos.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Você está pronto toogo toohello [guia do usuário do Docker] e usar sua VM Docker. toocreate uma VM Docker habilitado no novo portal de hello, consulte [como toouse Olá extensão da VM Docker com hello Portal].
* Olá extensão VM Docker do Azure também oferece suporte a redação do Docker, que usa um tootake de arquivo YAML declarativa um aplicativo modelada desenvolvedor em qualquer ambiente e gerar uma implantação consistente. Consulte [Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[como toouse Olá extensão da VM Docker com hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[guia do usuário do Docker]:https://docs.docker.com/userguide/

[Introdução ao Docker e compor toodefine e executar um aplicativo de multi-contêiner em uma máquina virtual do Azure]:../docker-compose-quickstart.md
