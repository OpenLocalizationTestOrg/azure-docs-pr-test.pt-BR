---
title: "agentes de VM do Azure aaaUse para integração contínua com Jenkins."
description: "Agentes de VM do Azure como Jenkins secundários."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Use agentes de VM do Azure para a integração contínua com Jenkins.

Este guia de início rápido mostra como toouse Olá toocreate de plug-in de agentes de VM do Azure Jenkins um agente do Linux (Ubuntu) sob demanda no Azure.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de início rápido:

* Se você ainda não tiver um mestre Jenkins, você pode iniciar com hello [modelo de solução](install-jenkins-solution-template.md) 
* Consulte também[criar uma entidade de serviço do Azure com o Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) se você ainda não tiver uma entidade de serviço do Azure.

## <a name="install-azure-vm-agents-plugin"></a>Instale o plug-in de agentes da VM do Azure

Se você iniciar da saudação [solução modelo](install-jenkins-solution-template.md), plug-in do hello Azure VM Agent está instalado no mestre de Jenkins hello.

Caso contrário, instalar Olá **agentes de VM do Azure** plug-in de dentro do painel de controle do hello Jenkins.

## <a name="configure-hello-plugin"></a>Configurar o plug-in de saudação

* No painel do Jenkins hello, clique em **Jenkins Gerenciar -> configurar o sistema ->**. Role toohello inferior da página de saudação e localize a seção de Olá Olá suspensa **adicionar nova nuvem**. No menu de saudação, selecione **agentes de VM do Microsoft Azure**
* Selecione uma conta existente na lista suspensa do hello credenciais do Azure.  tooadd um novo **entidade de serviço do Microsoft Azure,** digite Olá valores a seguir: ID de assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0.

![Credenciais do Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Clique em **Verificar configuração** toomake-se de que perfil Olá a configuração está correta.
* Salvar configuração hello e continuar toohello próxima etapa.

## <a name="template-configuration"></a>Configuração do modelo

### <a name="general-configuration"></a>Configuração geral
Em seguida, configure um modelo para uso toodefine um agente de VM do Azure. 

* Clique em **adicionar** tooadd um modelo. 
* Forneça um nome para o seu novo modelo. 
* Rótulo de hello, digite "ubuntu." Esse rótulo é usado durante a configuração de trabalho hello.
* Selecione região desejada Olá Olá na caixa de combinação.
* Selecione Olá desejada do tamanho da VM.
* Especifique o nome de conta de armazenamento do Azure hello ou deixe em branco toouse Olá padrao "jenkinsarmst".
* Especifique o tempo de retenção de saudação em minutos. Essa configuração define o número de saudação de minutos que Jenkins pode aguardar antes de excluir automaticamente um agente ocioso. Especifique 0 se não quiser toobe agentes ocioso excluído automaticamente.

![Configuração geral](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Configuração de imagem

toocreate um agente do Linux (Ubuntu), selecione **referência da imagem** e use Olá seguinte configuração de exemplo. Consulte também[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) para hello Azure mais recente com suporte a imagens.

* Publicador de imagem: Canonical
* Oferta de imagem: UbuntuServer
* Sku de imagem: 14.04.5-LTS
* Versão da imagem: mais recente
* Tipo de sistema operacional: Linux
* Inicie o método: SSH
* Forneça credenciais de administrador
* Para o script de inicialização de VM, digite:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuração de imagem](./media/jenkins-azure-vm-agents/image-config.png)

* Clique em **Verificar modelo** tooverify configuração de saudação.
* Clique em **Salvar**.

## <a name="create-a-job-in-jenkins"></a>Crie um trabalho no Jenkins

* No painel do Jenkins hello, clique em **Novo Item**. 
* Insira um nome e selecione **Projeto Freestyle** e clique em **Ok**.
* Em Olá **geral** , selecione "Restringir onde o projeto pode ser executado" e digite "ubuntu" na expressão de rótulo. Agora, você verá "ubuntu" no menu suspenso de saudação.
* Clique em **Salvar**.

![Configure o trabalho](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Compile o seu novo projeto

* Volte toohello Jenkins painel.
* Novo trabalho de saudação de atalho que você criou, clique em **compilar agora**. Uma compilação é iniciada. 
* Após a conclusão da compilação hello, ir muito**saída de Console**. Você verá que a compilação de saudação foi executada remotamente no Azure.

![Saída do console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Referência

* Vídeo de sexta-feira do Azure: [Integração contínua com Jenkins usando agentes de VM do Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* Opções de configuração e as informações de suporte: [Wiki de plug-in do Jenkins de agente de VM do Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

