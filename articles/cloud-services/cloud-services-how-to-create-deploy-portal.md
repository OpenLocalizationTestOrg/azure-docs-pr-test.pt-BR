---
title: "Como criar e implantar um serviço de nuvem | Microsoft Docs"
description: "Saiba como criar e implantar um serviço de nuvem usando o portal do Azure."
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
ms.openlocfilehash: 020e2996f40ed4a48affd3776e44e382c40cb3c0
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a>Como criar e implantar um serviço de nuvem
O portal do Azure oferece duas maneiras de criar e implantar um serviço de nuvem: *Criação Rápida* e *Criação Personalizada*.

Este artigo explica como usar o método Criação Rápida para criar um novo serviço de nuvem e usar **Carregar** para carregar e implantar um pacote de serviço de nuvem no Azure. Ao usar esse método, o Portal do Azure disponibiliza links convenientes para o cumprimento de todos os requisitos quando você precisar. Se você estiver pronto para implantar o serviço de nuvem ao criá-lo, é possível usar ambos ao mesmo tempo usando a Criação Personalizada.

> [!NOTE]
> Se você planeja publicar o serviço de nuvem do VSTS (Visual Studio Team Services), use a Criação Rápida e configure a publicação do VSTS no Início Rápido do Azure ou no painel. Para saber mais, confira [Entrega contínua no Azure usando Visual Studio Team Services][TFSTutorialForCloudService] ou confira a ajuda da página **Início Rápido**.
>
>

## <a name="concepts"></a>Conceitos
Três componentes são necessários para implantar um aplicativo como um serviço de nuvem no Azure:

* **Definição de serviço**  
  O arquivo de definição de serviço de nuvem (.csdef) define o modelo de serviço, inclusive o número de funções.
* **Configuração de serviço**  
  O arquivo de configuração de serviço de nuvem (.cscfg) fornece as configurações para o serviço de nuvem e as funções individuais, inclusive o número de instâncias de função.
* **Pacote de serviço**  
  O pacote de serviço (.cspkg) contém o código do aplicativo, as configurações e o arquivo de definição de serviço.

Você pode saber mais sobre eles e sobre como criar um pacote [aqui](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Preparação do aplicativo
Antes de poder implantar um serviço de nuvem, você deve criar o pacote do serviço de nuvem (arquivo .cspkg) do seu código do aplicativo e um arquivo de configuração do serviço de nuvem (.cscfg). O SDK do Azure fornece as ferramentas para preparar os arquivos exigidos para a implantação. Você pode instalar o SDK da página de [downloads de Azure](https://azure.microsoft.com/downloads/) no idioma em que você preferir desenvolver seu código do aplicativo.

Três recursos de serviço de nuvem precisam de configurações especiais antes que você exporte um pacote de serviço:

* Se você desejar implantar um serviço de nuvem que usa protocolo SSL para a criptografia de dados, [configure seu aplicativo](cloud-services-configure-ssl-certificate-portal.md#modify) para SSL.
* Se você desejar configurar conexões de área de trabalho remota para as instâncias de função, [configure as funções](cloud-services-role-enable-remote-desktop-new-portal.md) para Área de Trabalho Remota.
* Se você desejar configurar o monitoramento detalhado para o seu serviço de nuvem, habilite o Diagnóstico do Azure para o serviço de nuvem. *Monitoramento mínimo* (o nível de monitoramento padrão) usa contadores de desempenho coletados dos sistemas operacionais do host para as instâncias de função (máquinas virtuais). *Monitoramento detalhado* coleta métricas adicionais baseadas nos dados de desempenho nas instâncias de função para habilitar uma análise mais próxima dos problemas que ocorrem durante o processamento do aplicativo. Para saber como habilitar o Diagnóstico do Azure, confira [Habilitando o diagnóstico no Azure](cloud-services-dotnet-diagnostics.md).

Para criar um serviço de nuvem com implantações de funções Web ou de Trabalho, você deve [criar o pacote de serviço](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Antes de começar
* Se você não instalou o SDK do Azure, clique em **Instalar SDK do Azure** para abrir a [página de Downloads do Azure](https://azure.microsoft.com/downloads/)e baixar o SDK para o idioma em que você preferir desenvolver seu código. (Você terá uma oportunidade de fazer isso posteriormente).
* Se alguma instância de função precisar de certificados, crie-os. Os serviços de nuvem requerem um arquivo .pfx e uma chave privada. Você pode carregar os certificados para o Azure enquanto cria e implanta o serviço de nuvem.

## <a name="create-and-deploy"></a>Criar e implantar
1. Faça logon no [Portal do Azure](https://portal.azure.com/).
2. Clique em **Novo > Computação**, role para baixo e clique em **Serviço de Nuvem**.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Na nova folha **Serviço de Nuvem**, insira um valor para o **Nome DNS**.
4. Crie um novo **Grupo de Recursos** ou selecione um existente.
5. Selecione um **Local**.
6. Clique em **Pacote**. Isso abrirá a folha **Carregar um pacote** . Preencha os campos obrigatórios. Se alguma das funções contiver uma única instância, verifique se **Implantar mesmo se uma ou mais funções contiverem uma única instância** está marcado.
7. Verifique se a opção **Iniciar implantação** está selecionada.
8. Clique em **OK** que fechará a folha **Carregar um pacote**.
9. Se você não tiver nenhum certificado para adicionar, clique em **Criar**.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Carregar um certificado
Se o pacote de implantação tiver sido [configurado para usar certificados](cloud-services-configure-ssl-certificate-portal.md#modify), você poderá carregar o certificado agora.

1. Selecione **Certificados** e na folha **Adicionar certificados**, selecione o arquivo .pfx do certificado SSL, em seguida, forneça a **Senha** para o certificado,
2. Clique em **Anexar certificado**, em seguida, clique em **OK** na folha **Adicionar certificados**.
3. Clique em **Criar** na folha **Serviço de Nuvem**. Quando a implantação alcançar o status **Pronto** , será possível passar às próximas etapas.

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Verifique se a implantação foi concluída com êxito
1. Clique na instância do serviço de nuvem.

    O status deve mostrar que o serviço está **Executando**.
2. Em **Essentials**, clique na **URL do Site** para abrir o serviço de nuvem em um navegador da Web.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).
