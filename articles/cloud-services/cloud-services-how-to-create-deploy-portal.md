---
title: "aaaHow toocreate e implantar um serviço de nuvem | Microsoft Docs"
description: "Saiba como toocreate e implantar um serviço de nuvem usando Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Como toocreate e implantar um serviço de nuvem
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-create-deploy-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-create-deploy.md)
>
>

Olá portal do Azure fornece duas maneiras para você toocreate e implantar um serviço de nuvem: *criação rápida* e *criação personalizada*.

Este artigo explica como toouse Olá toocreate de método rápido criar um novo serviço de nuvem e, em seguida, usar **carregar** tooupload e implantar um pacote de serviço de nuvem no Azure. Quando você usar esse método, Olá portal do Azure torna disponível links convenientes para a conclusão de todos os requisitos conforme você avança. Se você estiver pronto toodeploy sua nuvem de serviço quando você criá-lo, você pode fazer ao Olá mesmo tempo usando criação personalizada.

> [!NOTE]
> Se você planejar toopublish seu serviço de nuvem do Visual Studio Team Services (VSTS), usar a criação rápida e, em seguida, configure a publicação do VSTS do painel de início rápido do Azure ou Olá Olá. Para obter mais informações, consulte [tooAzure entrega contínua, usando o Visual Studio Team Services][TFSTutorialForCloudService], ou consulte a Ajuda para Olá **início rápido** página.
>
>

## <a name="concepts"></a>Conceitos
Três componentes são necessário toodeploy um aplicativo como um serviço de nuvem no Azure:

* **Definição de serviço**  
  arquivo de definição de serviço de nuvem da saudação (. csdef) define o modelo de serviço hello, incluindo o número de funções hello.
* **Configuração de serviço**  
  arquivo de configuração de serviço de nuvem da saudação (. cscfg) fornece definições de configuração para o serviço de nuvem hello e funções individuais, incluindo Olá número de instâncias de função.
* **Pacote de serviço**  
  pacote de serviço da saudação (. cspkg) contém o código do aplicativo hello e configurações e o arquivo de definição de serviço hello.

Você pode aprender mais sobre essas e como um pacote de toocreate [aqui](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Preparação do aplicativo
Antes de implantar um serviço de nuvem, você deve criar o pacote de serviço de nuvem hello (. cspkg) do seu código de aplicativo e um arquivo de configuração de serviço de nuvem (. cscfg). Olá SDK do Azure fornece ferramentas para preparar a esses arquivos de implantação necessária. Você pode instalar o SDK de saudação do hello [Downloads do Azure](https://azure.microsoft.com/downloads/) página, na linguagem de saudação em que você preferir toodevelop seu código de aplicativo.

Três recursos de serviço de nuvem precisam de configurações especiais antes que você exporte um pacote de serviço:

* Se você quiser toodeploy um serviço de nuvem que usa o protocolo (SSL) para criptografia de dados, [configurar seu aplicativo](cloud-services-configure-ssl-certificate-portal.md#modify) para SSL.
* Se você quiser instâncias de toorole de conexões de área de trabalho remota tooconfigure, [configurar funções hello](cloud-services-role-enable-remote-desktop-new-portal.md) para área de trabalho remota.
* Se você quiser tooconfigure detalhado de monitoramento para seu serviço de nuvem, habilite o diagnóstico do Azure para serviço de nuvem hello. *Monitoramento mínimo* (Olá nível padrão de monitoração) usa contadores de desempenho coletados a partir de sistemas operacionais do hello host para instâncias de função (máquinas virtuais). *O monitoramento detalhado* coleta métricas adicionais com base nos dados de desempenho em Olá função instâncias tooenable uma análise mais próxima dos problemas que ocorrem durante o processamento do aplicativo. toofind como tooenable diagnóstico do Azure, consulte [habilitando diagnósticos no Azure](cloud-services-dotnet-diagnostics.md).

toocreate um serviço de nuvem com implantações de funções web ou funções de trabalho, você deve [criar pacote de serviço Olá](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Antes de começar
* Se você ainda não instalou Olá SDK do Azure, clique em **instalar SDK do Azure** tooopen Olá [página Downloads do Azure](https://azure.microsoft.com/downloads/)e, em seguida, baixe Olá SDK para o idioma de saudação em que você preferir toodevelop seu código. (Você terá uma oportunidade toodo isso mais tarde.)
* Se quaisquer instâncias de função exigem um certificado, crie certificados hello. Os serviços de nuvem requerem um arquivo .pfx e uma chave privada. Você pode carregar Olá certificados tooAzure como criar e implantar o serviço de nuvem hello.

## <a name="create-and-deploy"></a>Criar e implantar
1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **Novo > computação**e, em seguida, role para baixo clique tooand **serviço de nuvem**.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Em Olá novo **serviço de nuvem** folha, insira um valor para Olá **nome DNS**.
4. Crie um novo **Grupo de Recursos** ou selecione um existente.
5. Selecione um **Local**.
6. Clique em **Pacote**. Isso abrirá o hello **carregar um pacote** folha. Preencha os campos de saudação necessário. Se alguma das funções contiver uma única instância, verifique se **Implantar mesmo se uma ou mais funções contiverem uma única instância** está marcado.
7. Verifique se a opção **Iniciar implantação** está selecionada.
8. Clique em **Okey** que fechará Olá **carregar um pacote** folha.
9. Se você não tem qualquer tooadd de certificados, clique em **criar**.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Carregar um certificado
Se o pacote de implantação foi [configurado certificados toouse](cloud-services-configure-ssl-certificate-portal.md#modify), você pode carregar o certificado de saudação agora.

1. Selecione **certificados**e em Olá **adicionar certificados** folha, selecione o arquivo de. pfx de certificado SSL hello e forneça Olá **senha** certificado Olá,
2. Clique em **anexar certificado**e, em seguida, clique em **Okey** em Olá **adicionar certificados** folha.
3. Clique em **criar** em Olá **serviço de nuvem** folha. Quando a implantação de saudação atingiu Olá **pronto** status, você poderá toohello próximas etapas.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Verifique se a implantação foi concluída com êxito
1. Clique em instância de serviço de nuvem hello.

    Hello status deve mostrar que o serviço de saudação **executando**.
2. Em **Essentials**, clique em Olá **URL do Site** tooopen sua nuvem de serviço em um navegador da web.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).
