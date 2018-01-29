---
title: "Tutorial do Registro de Contêiner do Azure - Implantar o aplicativo Web do Registro de Contêiner do Azure"
description: "Implante um aplicativo Web baseado em Linux usando uma imagem de contêiner de um registro de contêiner do Azure replicado geograficamente. Parte dois de uma série de três partes."
services: container-registry
author: mmacy
manager: timlt
ms.service: container-registry
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: d775a17cb8069a7521788d850d7d52b92cc67526
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="deploy-web-app-from-azure-container-registry"></a>Implantar aplicativo Web do Registro de Contêiner do Azure

Esta é a parte três de uma série de tutoriais de três partes. Na [parte um](container-registry-tutorial-prepare-registry.md), foi criado um registro de contêiner replicado geograficamente privado, e uma imagem de contêiner foi criada da origem e enviado por push para o registro. Neste artigo, você pode implantar o contêiner em duas instâncias de Aplicativo Web em duas regiões diferentes do Azure para aproveitar o aspecto de fechamento de rede do registro replicado geograficamente.

Neste tutorial, parte dois da série:

> [!div class="checklist"]
> * Implantar uma imagem de contêiner em duas instâncias de *Aplicativos Web para Contêineres*
> * Verificar o aplicativo implantado

Se você ainda não tiver criado um registro replicado geograficamente e enviado por push a imagem do aplicativo de exemplo em contêineres no registro, retorne ao tutorial anterior na série, [Preparar um registro de contêiner do Azure replicado geograficamente](container-registry-tutorial-prepare-registry.md).

Na próxima parte da série, você atualiza o aplicativo e envia por push uma nova imagem de contêiner para o registro. Por fim, você navega até cada instância de Aplicativo Web em execução para ver a alteração automaticamente refletida em ambos, mostrando a replicação geográfica do Registro de Contêiner do Azure e webhooks em ação.

## <a name="automatic-deployment-to-web-apps-for-containers"></a>Implantação automática em Aplicativos Web para Contêineres

O Registro de Contêiner do Azure oferece suporte para a implantação de aplicativos em contêineres diretamente para [Aplicativos Web para Contêineres](../app-service/containers/index.yml). Neste tutorial, você pode usar o portal do Azure para implantar a imagem de contêiner criada no tutorial anterior para dois planos de aplicativos Web localizados em diferentes regiões do Azure.

Quando você implanta um aplicativo web de uma imagem de contêiner no registro, e você tem um registro de replicação geográfica na mesma região, o Registro de Contêiner do Azure cria um [webhook](container-registry-webhook.md) de implantação de imagem para você. Quando você enviar por push uma nova imagem para o repositório de contêiner, o webhook seleciona a alteração e implanta automaticamente a nova imagem de contêiner para seu aplicativo Web.

## <a name="deploy-a-web-app-for-containers-instance"></a>Implantar uma instância de Aplicativo Web para Contêineres

Nesta etapa, você cria uma instância de Aplicativo Web para Contêineres na região *Oeste dos EUA*.

Entre no [portal do Azure](https://portal.azure.com) e navegue até o registro que você criou no tutorial anterior.

Selecione **Repositórios** > **acr-helloworld**, clique com o botão direito do mouse na marca **v1** em **Marcas** e selecione **Implantar no aplicativo Web**.

![Implantar no serviço de aplicativo no portal do Azure][deploy-app-portal-01]

No **Aplicativo Web para Contêineres** exibido, especifique os seguintes valores para cada configuração:

| Configuração | Valor |
|---|---|
| **Nome do Site** | Um nome global exclusivo para o aplicativo Web. Neste exemplo, usamos o formato `<acrName>-westus` para identificar facilmente o registro e a região de onde o aplicativo Web é implantado. |
| **Grupo de recursos** | **Usar existente** > `myResourceGroup` |
| **Localização/plano de serviço de aplicativo** | Crie um novo plano chamado `plan-westus` na região **Oeste dos EUA**. |
| **Imagem** | `acr-helloworld:v1`

Selecione **Criar** para provisionar o aplicativo Web para a região *Oeste dos EUA*.

![Aplicativo Web na configuração do Linux no portal do Azure][deploy-app-portal-02]

## <a name="view-the-deployed-web-app"></a>Exibir o aplicativo Web implantado

Quando a implantação for concluída, você poderá exibir o aplicativo em execução navegando até a URL no navegador.

No portal, selecione **Serviços de Aplicativos** e depois o aplicativo Web configurado na etapa anterior. Neste exemplo, o aplicativo Web é chamado de *uniqueregistryname-westus*.

Selecione a URL com hiperlink do aplicativo Web na parte superior direita da visão geral do **Serviço de Aplicativo** para exibir o aplicativo em execução no seu navegador.

![Aplicativo Web na configuração do Linux no portal do Azure][deploy-app-portal-04]

Depois que a imagem do Docker for implantada do seu registro de contêiner replicado geograficamente, o site exibirá uma imagem que representa a região do Azure que hospeda o registro do contêiner.

![Aplicativo Web implantado exibido em um navegador][deployed-app-westus]

## <a name="deploy-second-web-app-for-containers-instance"></a>Implantar a segunda instância de Aplicativo Web para Contêineres

Use o procedimento descrito na seção anterior para implantar um segundo aplicativo Web para a região *Leste dos EUA*. Em **Aplicativo Web para Contêineres**, especifique os seguintes valores:

| Configuração | Valor |
|---|---|
| **Nome do Site** | Um nome global exclusivo para o aplicativo Web. Neste exemplo, usamos o formato `<acrName>-eastus` para identificar facilmente o registro e a região de onde o aplicativo Web é implantado. |
| **Grupo de recursos** | **Usar existente** > `myResourceGroup` |
| **Localização/plano de serviço de aplicativo** | Crie um novo plano chamado `plan-eastus` na região **Leste dos EUA**. |
| **Imagem** | `acr-helloworld:v1`

Selecione **Criar** para provisionar o aplicativo Web para a região *Leste dos EUA*.

![Aplicativo Web na configuração do Linux no portal do Azure][deploy-app-portal-06]

## <a name="view-the-deployed-web-app"></a>Exibir o aplicativo Web implantado

Como antes, você pode exibir o aplicativo em execução navegando até a URL no navegador.

No portal, selecione **Serviços de Aplicativos** e depois o aplicativo Web configurado na etapa anterior. Neste exemplo, o aplicativo Web é chamado de *uniqueregistryname-eastus*.

Selecione a URL do hiperlink do aplicativo Web na parte superior direita da **visão geral do Serviço de Aplicativo** para exibir o aplicativo em execução no seu navegador.

![Aplicativo Web na configuração do Linux no portal do Azure][deploy-app-portal-07]

Depois que a imagem do Docker for implantada do seu registro de contêiner replicado geograficamente, o site exibirá uma imagem que representa a região do Azure que hospeda o registro do contêiner.

![Aplicativo Web implantado exibido em um navegador][deployed-app-eastus]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você implantou duas instâncias de Aplicativo Web para Contêineres de um registro de contêiner do Azure replicado geograficamente. Seguindo as etapas neste tutorial, você:

> [!div class="checklist"]
> * Foi implantada uma imagem de contêiner para duas instâncias de *Aplicativos Web para Contêineres*
> * Verificar o aplicativo implantado

Avance para o próximo tutorial para atualizar e então implante uma nova imagem de contêiner para o registro de contêiner, então verifique se os aplicativos Web em execução em ambas as regiões foram atualizados automaticamente.

> [!div class="nextstepaction"]
> [Implantar uma atualização para a imagem de contêiner replicado geograficamente](./container-registry-tutorial-deploy-update.md)

<!-- IMAGES -->
[deploy-app-portal-01]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-01.png
[deploy-app-portal-02]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-02.png
[deploy-app-portal-03]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-03.png
[deploy-app-portal-04]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-04.png
[deploy-app-portal-05]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-05.png
[deploy-app-portal-06]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-06.png
[deploy-app-portal-07]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-07.png
[deployed-app-westus]: ./media/container-registry-tutorial-deploy-app/deployed-app-westus.png
[deployed-app-eastus]: ./media/container-registry-tutorial-deploy-app/deployed-app-eastus.png