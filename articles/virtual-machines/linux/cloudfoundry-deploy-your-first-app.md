---
title: aaaDeploy seu primeiro tooCloud de aplicativo Foundry no Microsoft Azure | Microsoft Docs
description: Implantar um aplicativo tooCloud Foundry no Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Implantar seu primeiro tooCloud de aplicativo Foundry no Microsoft Azure

O [Cloud Foundry](http://cloudfoundry.org) é uma plataforma de aplicativos populares de software livre disponível no Microsoft Azure. Neste artigo, mostramos como toodeploy e gerenciar um aplicativo em nuvem Foundry em um ambiente do Azure.

## <a name="create-a-cloud-foundry-environment"></a>Criar um ambiente do Cloud Foundry

Há várias opções para a criação de um ambiente do Cloud Foundry no Azure:

- Saudação de uso [oferta Foundry essencial de nuvem] [ pcf-azuremarketplace] em hello Azure Marketplace toocreate um ambiente padrão que inclui PCF Ops Manager e hello Azure Service Broker. Você pode encontrar [concluir instruções] [ pcf-azuremarketplace-pivotaldocs] para implantar o marketplace Olá oferecem em Olá documentação crucial.
- Crie um ambiente personalizado [implantando o Pivotal Cloud Foundry manualmente][pcf-custom].
- [Implantar pacotes de nuvem Foundry do código-fonte aberto Olá diretamente] [ oss-cf-bosh] Configurando um [BOSH](http://bosh.io) diretor, uma VM que coordena a implantação de saudação do ambiente de nuvem Foundry hello.

> [!IMPORTANT] 
> Se você estiver implantando PCF de hello Azure Marketplace, anote Olá SYSTEMDOMAINURL e credenciais de administrador Olá necessário tooaccess Olá essencial Gerenciador de aplicativos, que são descritas no guia de implantação do marketplace hello. Eles é necessário toocomplete neste tutorial. Para implantações do marketplace, Olá SYSTEMDOMAINURL está Olá formulário https://system. *endereço ip*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Conecte-se toohello controlador da nuvem

Olá controlador da nuvem é o ambiente de nuvem Foundry de tooa de ponto de entrada primária de Olá para implantar e gerenciar aplicativos. núcleo de saudação API de controlador de nuvem (CCAPI) é uma API REST, mas está acessível por meio de várias ferramentas. Nesse caso, estamos interagir com ele por meio de saudação [nuvem Foundry CLI][cf-cli]. Você pode instalar Olá CLI no Linux, MacOS ou Windows, mas se você preferir não tooinstall, ele está disponível pré-instalado em Olá [Shell de nuvem do Azure][cloudshell-docs].

toolog, preceda `api` toohello SYSTEMDOMAINURL que você obteve da implantação do marketplace hello. Desde que a implantação padrão de saudação usa um certificado autoassinado, você também deve incluir Olá `skip-ssl-validation` alternar.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Você está toolog solicitada no toohello controlador da nuvem. Use credenciais de conta de administrador de saudação que você copiou de etapas de implantação do marketplace hello.

Nuvem Foundry fornece *organizações* e *espaços* como equipes de saudação tooisolate namespaces e ambientes em uma implantação compartilhada. Olá implantação do marketplace PCF inclui padrão Olá *sistema* organizacional e um conjunto de espaços toocontain Olá base componentes criados, como serviço de dimensionamento automático hello e hello Azure do service broker. Por enquanto, escolha Olá *sistema* espaço.


## <a name="create-an-org-and-space"></a>Criar uma organização e um espaço

Se você digitar `cf apps`, verá um conjunto de aplicativos do sistema que foram implantados no espaço de sistema hello dentro Olá sistema org 

Você deve manter Olá *sistema* org reservado para aplicativos do sistema, portanto, crie um toohouse org e espaço de nosso aplicativo de exemplo.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Use Olá destino comando tooswitch toohello nova organização e espaço:

```bash
cf target -o testorg -s dev
```

Agora, quando você implanta um aplicativo, ele é criado automaticamente no espaço e Olá org de novo. tooconfirm atualmente, há nenhum aplicativo hello novo org/espaço, digite `cf apps` novamente.

> [!NOTE] 
> Para obter mais informações sobre organizações e espaços, e como eles podem ser usados para controle de acesso baseado em função (RBAC), consulte Olá [documentação nuvem Foundry][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Implantar um aplicativo

Vamos usar um aplicativo de nuvem Foundry de exemplo chamado Hello Spring nuvem, que é escrito em Java e com base em Olá [Spring Framework](http://spring.io) e [Spring inicialização](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Clonar Olá Olá Spring nuvem repositório

Olá aplicativo de exemplo Hello Spring nuvem está disponível no GitHub. Clone-tooyour ambiente e alterar para o novo diretório de saudação:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Criar um aplicativo hello

Usando o aplicativo hello compilação [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Implantar o aplicativo hello com cf envio por push

Você pode implantar a maioria dos aplicativos tooCloud Foundry usando Olá `push` comando:

```bash
cf push
```

Quando você *push* um aplicativo, nuvem Foundry detecta o tipo de saudação do aplicativo (neste caso, um aplicativo Java) e identifica as suas dependências (neste caso, Spring framework Olá). Em seguida, empacota tudo necessário toorun seu código em uma imagem de contêiner autônomo, conhecida como um *droplet*. Finalmente, agendas de nuvem Foundry Olá aplicativo em um dos computadores de Olá disponível no seu ambiente e cria uma URL em que você pode acessar, que está disponível na saída de saudação do comando hello.

![Saída do comando cf push][cf-push-output]

aplicativo em nuvem de spring de Olá toosee hello, abra Olá fornecido URL no navegador:

![Interface do usuário padrão do Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn mais sobre o que acontece durante `cf push`, consulte [como os aplicativos são preparados] [ cf-push-docs] em Olá documentação Foundry de nuvem.

## <a name="view-application-logs"></a>Exibir logs do aplicativo

Você pode usar logs de tooview Olá nuvem Foundry CLI para um aplicativo por seu nome:

```bash
cf logs hello-spring-cloud
```

Por padrão, a saudação registra o comando usa *final*, que mostra os novos logs como eles são gravados. toosee novos logs aparecerem, atualize Olá Olá de spring de nuvem aplicativo no navegador de saudação.

logs de tooview que já foram gravadas, adicionar Olá `recent` alternar:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Aplicativo hello de escala

Por padrão, `cf push` cria apenas uma única instância do aplicativo. tooensure alta disponibilidade e habilitar expansão para maior taxa de transferência, você geralmente deseja toorun mais de uma instância de seus aplicativos. Você pode expandir facilmente aplicativos já implantados usando Olá `scale` comando:

```bash
cf scale -i 2 hello-spring-cloud
```

Olá execução `cf app` comando no aplicativo hello mostra que a nuvem Foundry está criando outra instância do aplicativo hello. Após o início de aplicativo hello nuvem Foundry inicia automaticamente tooit do tráfego de balanceamento de carga.


## <a name="next-steps"></a>Próximas etapas

- [Saudação de leitura documentação Foundry de nuvem][cloudfoundry-docs]
- [Configurar o plug-in do Visual Studio Team Services Olá para nuvem Foundry][vsts-plugin]
- [Configurar Olá bocal de análise de Log do Microsoft para nuvem Foundry][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png