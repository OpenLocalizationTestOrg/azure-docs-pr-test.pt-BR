---
title: "aaaSet o proxy da web para o dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooconfigure web configurações de proxy para seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurar proxy da web para seu dispositivo StorSimple

## <a name="overview"></a>Visão geral

Este tutorial descreve como toouse do Windows PowerShell para StorSimple tooconfigure e modo de exibição web configurações de proxy para seu dispositivo StorSimple. configurações de proxy da web Hello são usadas pelo dispositivo do StorSimple Olá ao se comunicar com a nuvem de saudação. Um servidor de proxy da web é usada tooadd outra camada de segurança, filtrar conteúdo, cache tooease requisitos de largura de banda ou mesmo ajudar com a análise.

Guia de saudação neste tutorial se aplica apenas tooStorSimple 8000 series dispositivos físicos. Não há suporte para a configuração de proxy da Web em Olá StorSimple Appliance de nuvem (8010 e 8020).

O proxy Web é uma configuração _opcional_ para seu dispositivo StorSimple. Você pode configurar o proxy Web apenas por meio do Windows PowerShell para StorSimple. configuração de saudação é um processo de duas etapas da seguinte maneira:

1. Você primeiro configurar configurações de proxy da web por meio do Assistente de instalação de saudação ou o Windows PowerShell para StorSimple cmdlets.
2. Você, em seguida, habilitar configurações de proxy de web hello configurado por meio do Windows PowerShell para StorSimple cmdlets.

Após a conclusão da configuração do proxy web Olá, você pode exibir as configurações de proxy da web hello configurado no serviço do Gerenciador de dispositivos do Microsoft Azure StorSimple hello e saudação do Windows PowerShell para StorSimple.

Depois de ler este tutorial, você poderá:

* Configurar um proxy Web usando cmdlets e o assistente de instalação.
* Habilitar um proxy Web usando cmdlets.
* Exibir as configurações de proxy da web no portal do Azure de saudação.
* Solucionar erros durante a configuração do proxy Web.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurar o proxy Web por meio do Windows PowerShell para StorSimple

Você usar uma saudação configurações de proxy da web tooconfigure a seguir:

* Tooguide do Assistente de instalação você pelas etapas de configuração de saudação.
* Cmdlets do Windows PowerShell para StorSimple.

Cada um desses métodos é abordada em Olá seções a seguir.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Configurar o proxy da web por meio do Assistente de instalação de saudação

Use Olá instalação Assistente tooguide que você durante a saudação etapas de configuração de proxy da web. Execute Olá proxy de web tooconfigure as etapas a seguir em seu dispositivo.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>proxy de web tooconfigure por meio do Assistente de instalação de saudação

1. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo** e fornecer Olá **senha de administrador do dispositivo**. Digite o seguinte Olá comando toostart uma sessão do Assistente de instalação:
   
    `Invoke-HcsSetupWizard`
2. Se esse for Olá pela primeira vez que você usou o Assistente de instalação Olá para registro do dispositivo, você precisa tooconfigure todas as configurações de rede Olá necessário até que você alcance a configuração do proxy web hello. Se o dispositivo já está registrado, aceite todas as configurações de rede de saudação configurada até que você alcance a configuração do proxy web hello. No Assistente de instalação hello, quando solicitado tooconfigure web as configurações de proxy, digite **Sim**.
3. Para Olá **URL do Proxy Web**, especifique o endereço IP hello ou Olá nome de domínio totalmente qualificado (FQDN) do seu web proxy server e hello número da porta TCP que deseja que seu dispositivo toouse ao se comunicar com a nuvem de saudação. Use Olá formato a seguir:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Por padrão, o número de porta TCP 8080 é especificado.
4. Escolher tipo de autenticação hello como **NTLM**, **básica**, ou **nenhum**. Básica é a autenticação menos segura de Olá para configuração do servidor proxy hello. NT LAN Manager (NTLM) é um protocolo de autenticação altamente seguro e complexo que usa um sistema de mensagens de três vias (às vezes quatro se integridade adicional é necessária) tooauthenticate um usuário. autenticação de padrão de saudação é NTLM. Para obter mais informações, confira autenticação [Básica](http://hc.apache.org/httpclient-3.x/authentication.html) e [Autenticação NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Em Olá serviço do Gerenciador de dispositivos de StorSimple, gráficos de monitoramento de dispositivo de saudação não funcionam quando básica ou a autenticação NTLM é habilitada na configuração de servidor de proxy Olá para dispositivo hello. Para Olá toowork gráficos de monitoramento, você precisa tooensure autenticação está definida tooNONE.**
  
5. Se você habilitou a autenticação de hello, forneça um **nome de usuário de Proxy da Web** e um **senha do Proxy Web**. Você também precisa tooconfirm senha de saudação.
   
    ![Configurar o Proxy Web no Dispositivo1 do StorSimple](./media/storsimple-configure-web-proxy/IC751830.png)

Se você estiver registrando seu dispositivo para Olá a primeira vez, continue com o registro de saudação. Se seu dispositivo já foi registrado, o Assistente de saudação será encerrado. Olá configurado configurações são salvas.

Agora o proxy Web estará habilitado. Você pode ignorar Olá [habilitar o proxy web](#enable-web-proxy) etapa e vá diretamente muito[exibir configurações de proxy da web no portal do Azure de saudação](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configurar o proxy Web por meio de cmdlets do Windows PowerShell para StorSimple

Configurações de proxy uma maneira alternativa tooconfigure web é por meio de saudação do Windows PowerShell para StorSimple cmdlets. Execute Olá proxy de web tooconfigure as etapas a seguir.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>proxy de web tooconfigure por meio de cmdlets
1. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado, forneça Olá **senha de administrador do dispositivo**. Olá a senha padrão é `Password1`.
2. No prompt de comando hello, digite:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Digite e confirme a senha hello quando solicitado.
   
    ![Configurar o Proxy Web no Dispositivo3 do StorSimple](./media/storsimple-configure-web-proxy/IC751831.png)

proxy de web Hello agora está configurado e precisa toobe habilitado.

## <a name="enable-web-proxy"></a>Habilitar o proxy Web

O proxy Web está desabilitado por padrão. Depois de configurar configurações de proxy da web hello em seu dispositivo StorSimple, use saudação do Windows PowerShell para as configurações de proxy da web de saudação tooenable StorSimple.

> [!NOTE]
> **Essa etapa não será necessária se você usou o proxy da web do hello instalação Assistente tooconfigure. O proxy Web é habilitado automaticamente por padrão depois de uma sessão do assistente de instalação.**


Execute Olá seguindo as etapas no Windows PowerShell para o proxy do StorSimple tooenable web em seu dispositivo:

#### <a name="tooenable-web-proxy"></a>proxy de web tooenable
1. No menu do console serial hello, escolha a opção 1, **entrar com acesso completo**. Quando solicitado, forneça Olá **senha de administrador do dispositivo**. Olá a senha padrão é `Password1`.
2. No prompt de comando hello, digite:
   
    `Enable-HcsWebProxy`
   
    Agora você habilitou a configuração do proxy web hello em seu dispositivo StorSimple.
   
    ![Configurar o Proxy Web no Dispositivo4 do StorSimple](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a>Exibir configurações de proxy da web no portal do Azure de saudação

configurações de proxy da web Hello são configuradas por meio da interface do Windows PowerShell hello e não podem ser alteradas no portal de saudação. No entanto, você pode exibir essas configurações no portal de saudação. Execute Olá proxy de web tooview as etapas a seguir.

#### <a name="tooview-web-proxy-settings"></a>configurações de proxy da web tooview
1. Navegue muito**serviço do Gerenciador de dispositivos do StorSimple > dispositivos**. Selecione e clique em um dispositivo e, em seguida, ir muito**configurações do dispositivo > rede**.

    ![Clique em Rede](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. Em hello **as configurações de rede** folha, clique em Olá **proxy Web** lado a lado.

    ![Clique em proxy Web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. Em Olá **proxy Web** folha, configurações do proxy web revisão Olá configurado em seu dispositivo StorSimple.
   
    ![Exibir configurações do proxy Web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Erros durante a configuração de proxy Web

Se as configurações de proxy da web hello estão configuradas incorretamente, mensagens de erro são exibidas toohello usuário no Windows PowerShell para StorSimple. Olá, a tabela a seguir explica algumas dessas mensagens de erro, possíveis causas e ações recomendadas.

| N° de série | Código de erro HRESULT | Possível causa raiz | Ação recomendada |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Comando é executado no controlador passivo hello e não é capaz de toocommunicate com controlador ativo hello. |Execute o comando de saudação no controlador ativo Olá. comando de saudação toorun no controlador passivo hello, você deve corrigir conectividade de saudação do controlador passivo tooactive. Será necessário contatar o Suporte da Microsoft se essa conectividade for interrompida. |
| 2. |0x800710dd - identificador de operação de saudação não é válido |Não há suporte para as configurações de proxy no Dispositivo de Nuvem StorSimple. |Não há suporte para as configurações de proxy no Dispositivo de Nuvem StorSimple. Elas só podem ser configuradas em um dispositivo físico StorSimple. |
| 3. |0x80070057 - Parâmetro inválido |Um dos parâmetros de saudação fornecidos para as configurações de proxy de saudação não é válido. |Olá URI não é fornecido no formato correto. Use Olá formato a seguir:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - O servidor RPC não está disponível |causas de saudação é Olá seguinte:</br></br>O cluster não está ativo. </br></br>O serviço Datapath não está em execução.</br></br>Olá comando é executado no controlador passivo e não é capaz de toocommunicate com controlador ativo hello. |Envolver-se tooensure Microsoft Support que Olá cluster está ativo e o caminho de dados serviço está em execução.</br></br>Execute o comando de saudação do controlador ativo hello. Se desejar que o comando de saudação toorun no controlador passivo hello, você deve garantir que esse controlador passivo Olá pode se comunicar com o controlador ativo hello. Será necessário contatar o Suporte da Microsoft se essa conectividade for interrompida. |
| 5. |0x800706be - falha na chamada RPC |O cluster está inoperante. |Envolva Microsoft Support tooensure que Olá cluster está ativo. |
| 6. |0x8007138f - O recurso de cluster não foi encontrado |O recurso de cluster do serviço de plataforma não foi encontrado. Isso pode acontecer quando a instalação de saudação não está correta. |Talvez seja necessário tooperform uma redefinição de fábrica em seu dispositivo. Talvez seja necessário toocreate um recurso de plataforma. Contate o Suporte da Microsoft para as próximas etapas. |
| 7. |0x8007138c - O recurso de cluster não está online |Os recursos de cluster de plataforma ou caminho de dados não estão online. |Contato toohelp do Microsoft Support Certifique-se de que o recurso de serviço de plataforma e caminho de dados de saudação estão online. |

> [!NOTE]
> * Olá acima da lista de mensagens de erro não é exaustiva.
> * Configurações de proxy de tooweb relacionados de erros não serão exibidas no hello portal do Azure em seu serviço de Gerenciador de dispositivos do StorSimple. Se houver um problema com o proxy web após a configuração de hello, status do dispositivo Olá alterará muito**Offline** no portal clássico do hello. |

## <a name="next-steps"></a>Próximas etapas
* Se você tiver problemas ao implantar seu dispositivo ou configurações de proxy da web, consulte muito[solucionar problemas de implantação de dispositivo do StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn como toouse Olá serviço do Gerenciador de dispositivos de StorSimple, ir muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

