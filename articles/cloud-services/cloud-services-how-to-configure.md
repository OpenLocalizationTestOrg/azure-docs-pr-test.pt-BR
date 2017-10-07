---
title: "aaaHow tooconfigure um serviço de nuvem (portal clássico) | Microsoft Docs"
description: "Saiba como os serviços de nuvem tooconfigure no Azure. Aprenda a configuração do serviço de nuvem tooupdate hello e configurar instâncias de toorole de acesso remoto."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Como os serviços de nuvem tooConfigure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-configure-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-configure.md)
> 
> 

Você pode definir configurações de hello mais comumente usada para um serviço de nuvem no hello portal clássico do Azure. Ou, se desejar tooupdate seus arquivos de configuração diretamente, baixar um tooupdate de arquivo de configuração de serviço e, em seguida, carregar Olá atualizado de arquivo e atualização Olá serviço de nuvem com as alterações de configuração de saudação. De qualquer forma, as atualizações de configuração de saudação são enviados por push tooall instâncias de função.

Olá portal clássico do Azure também permite que você muito[habilitar Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure](cloud-services-role-enable-remote-desktop.md)

Azure pode apenas certifique-se de 99,95% de disponibilidade durante a saudação atualizações de configuração se você tem pelo menos duas instâncias de função para cada função. Que permite que uma máquina virtual tooprocess cliente solicitações enquanto outros hello está sendo atualizada. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Alterar um serviço de nuvem
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **configurar**.
   
    ![Página de configuração](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Em Olá **configurar** página, você pode configurar o monitoramento, atualização de configurações de função e escolha Olá sistema operacional e família para instâncias de função. 
2. Em **monitoramento**, Olá conjunto tooVerbose nível de monitoramento ou mínima e configurar Olá cadeias de conexão de diagnóstico que são necessárias para o monitoramento detalhado.
3. Para funções de serviço (agrupadas por função), você pode atualizar Olá configurações a seguir:
   
    * **Configurações de** modificar valores hello diverso de definições de configuração que são especificados em Olá *ConfigurationSettings* elementos Olá serviço (. cscfg) do arquivo de configuração.

    * **Certificados**  
        Alteração Olá impressão digital do certificado que está sendo usada na criptografia SSL para uma função. toochange um certificado, primeiro você deve carregar Olá novo certificado (em Olá **certificados** página). Em seguida, atualize impressão digital de saudação na cadeia de caracteres do certificado Olá exibida nas configurações de função hello.
4. Em **sistema operacional**, você pode alterar a versão para instâncias de função ou família de sistemas operacionais hello, ou escolha **automático** tooenable as atualizações automáticas de versão do sistema operacional atual hello. configurações do sistema operacional Olá aplicam tooweb funções e funções de trabalho, mas não afetam as máquinas virtuais.
   
    Durante a implantação, versão do sistema operacional mais recente Olá é instalado em todas as instâncias de função e sistemas operacionais de saudação são atualizados automaticamente por padrão. 
   
    Se você precisar para seu toorun de serviço de nuvem em uma versão diferente do sistema operacional devido aos requisitos de compatibilidade em seu código, você pode escolher uma família de sistema operacional e versão. Quando você escolhe uma versão específica do sistema operacional, atualizações automática do sistema operacional para o serviço de nuvem Olá são suspensos. Você precisará tooensure sistemas operacionais de saudação receber atualizações.
   
    Se você resolver todos os problemas de compatibilidade com seus aplicativos com a versão do sistema operacional mais recente hello, você pode habilitar atualizações automáticas do sistema operacional pela versão de sistema operacional Olá configuração muito**automática**. 
   
    ![Definições do sistema operacional](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave as configurações e enviá-las a instâncias de função toohello, clique em **salvar**. (Clique em **descartar** alterações de saudação toocancel.) **Salvar** e **descartar** são adicionados a barra de comandos toohello depois de alterar uma configuração.

## <a name="update-a-cloud-service-configuration-file"></a>Atualizar um arquivo de configuração de serviço de nuvem
1. Baixe um arquivo de configuração de serviço de nuvem (. cscfg) com a configuração atual de saudação. Em Olá **configurar** para serviço de nuvem hello, clique em **baixar**. Em seguida, clique em **salvar**, ou clique em **Salvar como** toosave arquivo de saudação.
2. Depois de atualizar o arquivo de configuração de serviço hello, carregar e aplicar as atualizações de configuração de saudação:
   
   1. Em Olá **configurar** , clique em **carregar**.
      
       ![Carregamento da configuração](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. Em **arquivo de configuração**, use **procurar** tooselect Olá atualizado o arquivo. cscfg.
   3. Se seu serviço de nuvem contém as funções que têm apenas uma instância, selecione Olá **aplicar configuração mesmo se uma ou mais funções contiverem uma única instância** caixa de seleção tooenable atualizações de configuração Olá para Olá funções tooproceed.
      
       A menos que você defina no mínimo duas instâncias de cada função, o Azure não poderá garantir ao menos 99,95 por cento de disponibilidade do seu Serviço de Nuvem durante as atualizações da configuração do serviço. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).
   4. Clique em **OK** (marca de seleção). 

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage.md).
* [Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure](cloud-services-role-enable-remote-desktop.md)
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate.md).

