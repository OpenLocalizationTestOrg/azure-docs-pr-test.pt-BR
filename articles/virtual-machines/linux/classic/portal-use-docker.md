---
title: "aaaUsing extensão da VM Docker para Linux | Microsoft Docs"
description: "Descreve como toocreate máquinas virtuais do Azure que são hosts de docker usando Olá CLI do Azure no modelo de implantação clássico e extensões de máquinas virtuais do Azure hello e Docker."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Usando Olá extensão da VM Docker com hello portal clássico do Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

[Docker](https://www.docker.com/) é uma saudação mais populares abordagens de virtualização que usa [contêineres Linux](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como um modo de isolamento de dados e computação em recursos compartilhados. Você pode usar a extensão de VM Docker Olá gerenciado pelo [agente Linux do Azure] toocreate uma VM Docker que hospeda qualquer número de contêineres para seus aplicativos no Azure.

> [!NOTE]
> Este tópico descreve como toocreate uma VM Docker do hello portal clássico do Azure. toosee como toocreate uma VM Docker na linha de comando hello, consulte [como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)]. toosee uma discussão detalhada sobre contêineres e suas vantagens, consulte Olá [Docker alto nível de quadro](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Criar uma nova VM da Galeria de imagens de saudação
Olá primeira etapa exige uma VM do Azure de uma imagem do Linux que oferece suporte a saudação extensão da VM Docker, usando uma imagem do Ubuntu 14.04 LTS de saudação Galeria de imagens como uma imagem de servidor de exemplo e área de trabalho do Ubuntu 14.04 como um cliente. No portal de saudação, clique em **+ novo** no hello inferior esquerda canto toocreate uma nova instância de máquina virtual e selecione uma imagem Ubuntu 14.04 LTS de seleções de saudação disponíveis ou de saudação concluir a Galeria de imagens, conforme mostrado abaixo.

> [!NOTE]
> Atualmente, apenas imagens de Ubuntu 14.04 LTS mais recentes do que de julho de 2014 aceita Olá extensão da VM Docker.
> 
> 

![Criar uma nova imagem Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Criar certificados Docker
Após Olá que VM foi criada, certifique-se de que o Docker é instalado no computador cliente. Para obter detalhes, confira [Instruções de instalação do Docker](https://docs.docker.com/installation/#installation).

Criar hello arquivos de certificado e a chave para comunicação do Docker de acordo com muito[Docker em execução com https] e colocá-los em Olá  **`~/.docker`**  diretório no computador cliente.

> [!NOTE]
> Olá extensão da VM Docker no portal de saudação atualmente requer credenciais que são codificados na base64.
> 
> 

Na linha de comando hello, use  **`base64`**  ou favorito outra codificação tópicos sobre a ferramenta toocreate codificado na base64. Fazer isso com um conjunto simple de arquivos de certificado e chave pode parecer semelhante toothis:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Adicionar Olá extensão da VM Docker
tooadd Olá extensão da VM Docker, localize a instância VM Olá criada e role para baixo demais**extensões** e clique toobring a extensões de VM, conforme mostrado abaixo.

> [!NOTE]
> Essa funcionalidade é suportada no portal de visualização de saudação apenas: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Adicionar uma extensão
Clique em Olá **+ adicionar** toodisplay Olá possíveis extensões de VM, você pode adicionar toothis VM.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Selecione Olá extensão da VM Docker
Escolha Olá extensão da VM Docker, que traz links importantes e descrição de Docker Olá, e, em seguida, clique em **criar** no procedimento de instalação do hello inferior toobegin hello.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Adicionar seus arquivos de certificado e de chaves:
Olá campos de formulário, insira versões codificada em base64 de saudação do seu certificado de autoridade de certificação, o certificado de servidor e a chave do servidor, conforme mostrado no gráfico a seguir de saudação.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Observe que (como saudação anterior imagem) Olá 2376 é preenchido por padrão. Você pode inserir qualquer ponto de extremidade aqui, mas Olá próximo passo será tooopen backup Olá correspondência de ponto de extremidade. Se você alterar o padrão de hello, verifique se tooopen backup Olá correspondência na próxima etapa de saudação do ponto de extremidade.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Adicionar Olá ponto de extremidade de comunicação de Docker
Ao exibir o grupo de recursos de saudação que você criou, selecione Olá grupo de segurança de rede associado a sua VM e clique em **regras de segurança de entrada** tooview Olá regras conforme mostrado aqui.

![](media/portal-use-docker/AddingEndpoint.png)

Clique em **+ adicionar** tooadd outra regra e no caso de padrão de saudação, insira um nome para o ponto de extremidade de saudação (neste exemplo, **Docker**) e 2376 'intervalo de porta de destino'. Definir mostrando de valor de protocolo hello **TCP**e clique em **Okey** toocreate regra de saudação.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Testar o cliente Docker e o host Docker do Azure
Localize e copie Olá nome de domínio da VM e na linha de comando de saudação do computador cliente, o tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (onde *dockerextension* é substituído pelo Olá subdomínio para sua VM).

resultado de saudação deve aparecer toothis semelhante:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Depois de concluir Olá acima etapas, agora você tem um host Docker totalmente funcional em execução em uma VM do Azure, configurado toobe conectado tooremotely de outros clientes.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
Você está pronto toogo toohello [guia do usuário do Docker] e usar sua VM Docker. Se você quiser tooautomate criando hosts de Docker em VMs do Azure por meio da interface de linha de comando, consulte [como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[como toouse Olá extensão da VM Docker do hello Azure Interface de linha de comando (CLI do Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux do Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[Docker em execução com https]:http://docs.docker.com/articles/https/
[guia do usuário do Docker]:https://docs.docker.com/userguide/
