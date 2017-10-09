---
title: aaaUpgrade PhoneFactor tooAzure servidor MFA | Microsoft Docs
description: "Introdução ao servidor Azure MFA ao atualizar do agente phonefactor anterior de saudação."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Atualizar Olá agente PhoneFactor tooAzure servidor multi-Factor Authentication
tooupgrade Olá PhoneFactor Agent V5. x ou mais antiga tooAzure servidor multi-Factor Authentication, desinstale Olá agente PhoneFactor e afiliado componentes primeiro. Olá, em seguida, o servidor multi-Factor Authentication e seus componentes afiliados podem ser instalados.

## <a name="uninstall-hello-phonefactor-agent"></a>Desinstalar Olá PhoneFactor Agent

1. Primeiro, faça backup do arquivo de dados do PhoneFactor hello. Olá instalação padrão é C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Se estiver instalado Olá Portal do usuário:
  1. Navegue toohello a pasta de instalação e faça backup do arquivo Web. config de saudação. Olá instalação padrão é c:\inetpub\wwwroot\phonefactor..

  2. Se você tiver adicionado o portal de toohello de temas personalizados, faz backup da pasta personalizada abaixo do diretório c:\inetpub\wwwroot\phonefactor\app_themes. de saudação.

  3. Desinstalar Olá Portal do usuário por meio de saudação agente PhoneFactor (disponível somente se instalado em Olá mesmo servidor Olá agente PhoneFactor) ou por meio de programas do Windows e recursos.

3. Se hello serviço Web aplicativos móveis é instalado:

  1. Vá toohello a pasta de instalação e faça backup do arquivo Web. config de saudação. Olá instalação padrão é c:\inetpub\wwwroot\phonefactorphoneappwebservice..

  2. Desinstale Olá móvel do serviço de aplicativo Web por meio de programas do Windows e recursos.

4. Se Olá SDK do serviço Web está instalado, desinstale-o por meio de saudação PhoneFactor Agent ou Windows programas e recursos.

5. Desinstale Olá PhoneFactor Agent por meio de programas do Windows e recursos.

## <a name="install-hello-multi-factor-authentication-server"></a>Instalar Olá servidor multi-Factor Authentication

Olá caminho de instalação é obtido do registro de saudação da instalação anterior do agente PhoneFactor Olá, para que ele deve ser instalado no hello mesmo local (por exemplo, C:\Program programas\phonefactor). As novas instalações terão um padrão diferente (por exemplo, C:\Arquivos de Programas\Servidor de Autenticação Multifator). Olá arquivo de dados deixado pelo Olá anterior do que phonefactor Agent deve ser atualizado durante a instalação, portanto, seus usuários e configurações ainda devem ser que lá após a instalação Olá novo servidor multi-Factor Authentication.

1. Se solicitado, ative Olá servidor multi-Factor Authentication e certifique-se de que ele está atribuído toohello grupo de replicação correto.

2. Se instalar o SDK do serviço Web foi instalado anteriormente, de saudação Olá novo SDK do serviço Web por meio de saudação Interface de usuário do multi-Factor Authentication Server.

  Olá padrão de nome do diretório virtual agora está **MultiFactorAuthWebServiceSdk** em vez de **PhoneFactorWebServiceSdk**. Se desejar que o nome anterior do toouse hello, você deve alterar o nome de saudação do diretório virtual Olá durante a instalação. Caso contrário, se você permitir Olá install toouse Olá novo nome padrão, você tem toochange Olá URL em todos os aplicativos que Olá referência toopoint do SDK do serviço Web (como Olá Portal do usuário e serviço Web aplicativos móveis) no local correto hello.

3. Se instalar Olá Portal do usuário foi instalado anteriormente no hello servidor PhoneFactor Agent, Olá novo Portal do usuário multi-Factor Authentication por meio de saudação Interface de usuário do multi-Factor Authentication Server.

  Olá padrão de nome do diretório virtual agora está **MultiFactorAuth** em vez de **PhoneFactor**. Se desejar que o nome anterior do toouse hello, você deve alterar o nome de saudação do diretório virtual Olá durante a instalação. Caso contrário, se você permitir Olá install toouse Olá novo nome padrão, clique ícone do Portal do usuário Olá no hello servidor multi-Factor Authentication e atualizar Olá URL do Portal do usuário na guia Configurações de saudação.

4. Se hello Portal do usuário e/ou o serviço Web aplicativos móveis foi instalado anteriormente em um servidor diferente do hello PhoneFactor Agent:

  1. Vá toohello local de instalação (por exemplo, C:\Program programas\phonefactor) e copiar um ou mais toohello de instaladores outro servidor. Há instaladores de 32 bits e 64 bits para Olá Portal do usuário e o serviço Web aplicativos móveis. Eles são chamados MultiFactorAuthenticationUserPortalSetupXX.msi e MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. Olá tooinstall Portal do usuário no servidor de web hello, abra um prompt de comando como administrador e execute o MultiFactorAuthenticationUserPortalSetupXX.msi.

    Olá padrão de nome do diretório virtual agora está **MultiFactorAuth** em vez de **PhoneFactor**. Se desejar que o nome anterior do toouse hello, você deve alterar o nome de saudação do diretório virtual Olá durante a instalação. Caso contrário, se você permitir Olá install toouse Olá novo nome padrão, clique ícone do Portal do usuário Olá no hello servidor multi-Factor Authentication e atualizar Olá URL do Portal do usuário na guia Configurações de saudação. Os usuários existentes necessitam toobe informado de saudação nova URL.

  3. Vá toohello local de instalação do Portal do usuário (por exemplo, C:\inetpub\wwwroot\MultiFactorAuth) e edite o arquivo Web. config de saudação. Copie os valores de Olá nas seções appSettings e applicationSettings de saudação do arquivo Web. config original que foi feito backup antes da atualização Olá no arquivo Web. config da nova hello. Se o novo nome de diretório virtual padrão Olá foi mantido durante a instalação Olá SDK do serviço Web, altere a URL de saudação no local correto do toohello de toopoint de seção do hello applicationSettings. Se outros padrões foram alterados no arquivo Web. config anterior de saudação, aplica as mesmas alterações toohello novo arquivo Web. config.

  4. Olá tooinstall serviço Web aplicativos móveis no servidor de web hello, abra um prompt de comando como administrador e execute Olá MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    Olá padrão de nome do diretório virtual agora está **MultiFactorAuthMobileAppWebService** em vez de **PhoneFactorPhoneAppWebService**. Se desejar que o nome anterior do toouse hello, você deve alterar o nome de saudação do diretório virtual Olá durante a instalação. Talvez você queira toochoose um toomake mais curto do nome fácil para os usuários finais a tootype em seus dispositivos móveis. Caso contrário, se você permitir Olá install toouse Olá novo nome padrão, clique Olá ícone de aplicativo móvel no hello servidor multi-Factor Authentication e atualizar Olá URL de serviço da Web de aplicativos móveis.

  5. Vá local de instalação do serviço Web aplicativos móveis toohello (por exemplo, C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) e edite o arquivo Web. config de saudação. Copie os valores de Olá nas seções appSettings e applicationSettings de saudação do arquivo Web. config original que foi feito backup antes da atualização Olá no arquivo Web. config da nova hello. Se o novo nome de diretório virtual padrão Olá foi mantido durante a instalação Olá SDK do serviço Web, altere a URL de saudação no local correto do toohello de toopoint de seção do hello applicationSettings. Se outros padrões foram alterados no arquivo Web. config anterior de saudação, aplica as mesmas alterações toohello novo arquivo Web. config.

## <a name="next-steps"></a>Próximas etapas

- [Instalar o portal de usuários Olá](multi-factor-authentication-get-started-portal.md) para Olá servidor Azure multi-Factor Authentication.

- [Configurar a autenticação do Windows](multi-factor-authentication-get-started-server-windows.md) para seus aplicativos. 
