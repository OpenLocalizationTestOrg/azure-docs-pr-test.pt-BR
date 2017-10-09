---
title: aaaConnect remotamente o dispositivo StorSimple tooyour | Microsoft Docs
description: Explica como tooconfigure seu dispositivo para o gerenciamento remoto e como tooconnect tooWindows PowerShell para StorSimple via HTTP ou HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Conectar-se remotamente dispositivo da série StorSimple 8000 do tooyour

## <a name="overview"></a>Visão geral

Você pode se conectar remotamente tooyour dispositivo por meio do Windows PowerShell. Ao se conectar dessa maneira, você não vê um menu. (Você verá um menu somente se você usar o console serial Olá em Olá dispositivo tooconnect.) Com a comunicação remota do Windows PowerShell, você pode se conectar runspace específico tooa. Você também pode especificar o idioma de exibição de saudação.

Para obter mais informações sobre como usar o Windows PowerShell remoting toomanage seu dispositivo, vá muito[usar o Windows PowerShell para StorSimple tooadminister seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).

Este tutorial explica como tooconfigure seu dispositivo para gerenciamento remoto e, em seguida, como tooconnect tooWindows PowerShell para StorSimple. Você pode usar HTTP ou HTTPS tooremotely conectar via Windows PowerShell. No entanto, quando você estiver decidindo como tooconnect tooWindows PowerShell para StorSimple, considere Olá informações a seguir:

* Conectando-se diretamente toohello console serial do dispositivo é seguro, mas conectar console serial do toohello em comutadores de rede não é. Seja cauteloso Olá dos riscos de segurança ao conectar-se o console serial do dispositivo toohello em comutadores de rede.
* Conectando por meio de uma sessão HTTP pode oferecer mais segurança do que conectar-se por meio do console serial Olá via rede hello. Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.
* Conectando por meio de uma sessão HTTPS com um certificado autoassinado é hello mais seguro e Olá opção recomendada.

Você pode se conectar remotamente toohello interface do Windows PowerShell. No entanto, os dispositivos de StorSimple tooyour acesso remoto por meio da interface do Windows PowerShell Olá não está habilitado por padrão. Você deve habilitar o gerenciamento remoto no dispositivo Olá primeiro e, em seguida, em Olá cliente que é usado tooaccess seu dispositivo.

etapas de saudação descritas neste artigo foram executadas em um sistema de host executando o Windows Server 2012 R2.

## <a name="connect-through-http"></a>Conectar-se por meio de HTTP

Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTP oferece mais segurança do que se conectam por meio do console de série de saudação do seu dispositivo StorSimple. Embora isso não é um método mais seguro Olá, é aceitável em redes confiáveis.

Você pode usar o hello Azure portal ou hello serial tooconfigure gerenciamento remoto do console. Selecione Olá procedimentos a seguir:

* [Usar o gerenciamento remoto do hello tooenable portal do Azure através de HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Depois de habilitar o gerenciamento remoto, use Olá seguindo o procedimento tooprepare saudação do cliente para uma conexão remota.

* [Prepare saudação do cliente para conexão remota](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a>Usar o gerenciamento remoto do hello tooenable portal do Azure através de HTTP

Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable portal do Azure via HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a>gerenciamento remoto de tooenable por meio de saudação portal do Azure

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Selecione **dispositivos** e selecione e clique em dispositivo Olá desejar tooconfigure para gerenciamento remoto. Vá muito**configurações do dispositivo > segurança**.
2. Em Olá **as configurações de segurança** folha, clique em **gerenciamento remoto**.
3. Em Olá **gerenciamento remoto** folha, defina **habilitar o gerenciamento remoto** muito**Sim**.
4. Agora você pode escolher tooconnect usando HTTP. (o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTP esteja selecionado.
   
   > [!NOTE]
   > A conexão por HTTP só será aceitável em redes confiáveis.
   
5. Clique em **Salvar** e, quando precisar confirmar, selecione **Sim**.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Usar o gerenciamento remoto do tooenable Olá console serial sobre HTTP
Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gerenciamento remoto de tooenable através do console serial do dispositivo Olá
1. No menu do console serial hello, selecione a opção 1. Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. No prompt de hello, digite:`Enable-HcsRemoteManagement –AllowHttp`
3. Você será notificado sobre vulnerabilidades de segurança de saudação do uso de dispositivo de toohello tooconnect HTTP. Quando solicitado, confirme digitando **Y**.
4. Verifique se o HTTP estiver habilitado digitando: `Get-HcsSystem`
5. Verifique se esse Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.
   
     ![HTTPS serial e HTTP habilitados](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Prepare saudação do cliente para conexão remota
Execute Olá seguindo as etapas no gerenciamento remoto do hello cliente tooenable.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>cliente de saudação tooprepare para conexão remota
1. Inicie uma sessão do Windows PowerShell como administrador.
2. Digite hello endereço IP do comando tooadd Olá da lista de hosts confiáveis do cliente do toohello dispositivo StorSimple Olá a seguir:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Substitua <*device_ip*> com o endereço IP de saudação do seu dispositivo, por exemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Digite o seguinte Olá credenciais do dispositivo Olá toosave em uma variável de comando: 
   
    ```
    $cred = Get-Credential
    ```
    
4. Na caixa de diálogo de saudação aparece:
   
   1. Nome de usuário do tipo hello neste formato: *device_ip\SSAdmin*.
   2. Digite a senha do administrador de dispositivo de saudação foi definida quando o dispositivo Olá foi configurado com o Assistente de instalação de saudação. a senha padrão Olá é *Password1*.
5. Inicie uma sessão do Windows PowerShell no dispositivo Olá digitando o seguinte comando:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate uma sessão do Windows PowerShell para uso com o dispositivo virtual do StorSimple hello, acrescente Olá `–Port` parâmetro e especifique a porta pública de saudação que você configurou na comunicação remota para o dispositivo Virtual StorSimple.
   
   
Neste ponto, você deve ter um dispositivo de toohello de sessão ativado de remoto do Windows PowerShell.
   
![PowerShell remoto usando HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Conectar-se por meio de HTTPS

Conectar tooWindows PowerShell para StorSimple por meio de uma sessão HTTPS é hello mais seguro e recomendado de método do dispositivo de Microsoft Azure StorSimple tooyour conectar remotamente. Olá procedimentos a seguir explica como tooset backup Olá seriais consoles e computadores clientes para que você possa usar HTTPS tooconnect tooWindows PowerShell para StorSimple.

Você pode usar o hello Azure portal ou hello serial tooconfigure gerenciamento remoto do console. Selecione Olá procedimentos a seguir:

* [Usar o gerenciamento remoto do hello tooenable portal do Azure via HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Usar o gerenciamento remoto do hello console serial tooenable via HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Depois de habilitar o gerenciamento remoto, use Olá seguindo o host de saudação tooprepare procedimentos para o gerenciamento remoto e conecte o dispositivo toohello do host remoto Olá.

* [Preparar o host Olá para gerenciamento remoto](#prepare-the-host-for-remote-management)
* [Conecte o dispositivo de toohello do host remoto Olá](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a>Usar o gerenciamento remoto do hello tooenable portal do Azure via HTTPS

Execute Olá seguindo as etapas no gerenciamento remoto do hello tooenable portal do Azure via HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a>gerenciamento remoto tooenable via HTTPS de saudação portal do Azure

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Selecione **dispositivos** e selecione e clique em dispositivo Olá desejar tooconfigure para gerenciamento remoto. Vá muito**configurações do dispositivo > segurança**.
2. Em Olá **as configurações de segurança** folha, clique em **gerenciamento remoto**.
3. Definir **habilitar o gerenciamento remoto** muito**Sim**.
4. Agora você pode escolher tooconnect usando HTTPS. (o padrão de saudação é tooconnect via HTTPS.) Certifique-se de que HTTPS esteja selecionado.
5. Clique em ... e em **Baixar Certificado de gerenciamento remoto**. Especifique um local toosave esse arquivo. Você precisará tooinstall este certificado no computador cliente ou host de saudação que você usará tooconnect toohello dispositivo.
6. Clique em **Salvar** e, quando precisar confirmar, clique em **Sim**.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Usar o gerenciamento remoto do hello console serial tooenable via HTTPS

Execute Olá seguindo as etapas no gerenciamento remoto do tooenable Olá dispositivo console serial.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gerenciamento remoto de tooenable através do console serial do dispositivo Olá
1. No menu do console serial hello, selecione a opção 1. Para obter mais informações sobre como usar o console serial Olá no dispositivo hello, ir muito[conectar tooWindows PowerShell para StorSimple por meio do console serial do dispositivo](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. No prompt de hello, digite:
   
     `Enable-HcsRemoteManagement`
   
    Isso deve habilitar HTTPS em seu dispositivo.
3. Verifique se o HTTP está habilitado digitando: 
   
     `Get-HcsSystem`
   
    Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello ilustração a seguir mostra essas configurações em PuTTY.
   
     ![HTTPS serial habilitado](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Da saída de saudação de `Get-HcsSystem`, copie Olá o número de série do dispositivo hello e salvá-lo para uso posterior.
   
   > [!NOTE]
   > número de série de saudação mapeia toohello nome CN no certificado de saudação.
   
5. Obtenha um certificado de gerenciamento remoto, digitando: 
   
     `Get-HcsRemoteManagementCert`
   
    Uma certificado semelhante toohello a seguir será exibida.
   
    ![Obter certificado de gerenciamento remoto](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiar informações de saudação no certificado de saudação do **---iniciar certificado---** muito**---concluir certificado---** em um editor de texto como bloco de notas e salve-o como um arquivo. cer. (Você copiará esse host remoto do arquivo tooyour quando você prepara o host hello.)
   
   > [!NOTE]
   > toogenerate um novo certificado, use Olá `Set-HcsRemoteManagementCert` cmdlet.
   
### <a name="prepare-hello-host-for-remote-management"></a>Preparar o host Olá para gerenciamento remoto

computador de host tooprepare Olá para uma conexão remota que usa uma sessão HTTPS, execute Olá procedimentos a seguir:

* [Arquivo de importação. cer de saudação no repositório de raiz de saudação do cliente hello ou host remoto](#to-import-the-certificate-on-the-remote-host).
* [Adicionar números de série do dispositivo de Olá toohello arquivo hosts em seu host remoto](#to-add-device-serial-numbers-to-the-remote-host).

Cada saudação anterior procedimentos, é descrito abaixo.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>certificado de saudação tooimport no host remoto Olá
1. Clique em arquivo. cer de saudação e selecione **Instalar certificado**. Isso inicia o hello Assistente de importação de certificado.
   
    ![Assistente para importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Em **Localização do repositório**, selecione **Computador Local** e, em seguida, clique em **Próximo**.
3. Selecione **colocar todos os certificados no hello repositório a seguir**e, em seguida, clique em **procurar**. Navegue toohello repositório de raiz do seu host remoto e, em seguida, clique em **próximo**.
   
    ![Assistente para importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Clique em **Concluir**. Será exibida uma mensagem que informa que Olá importação foi bem-sucedida.
   
    ![Assistente para importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>host remoto do toohello tooadd dispositivo números de série
1. Inicie o bloco de notas como administrador e, em seguida, abra o arquivo de hosts de saudação localizado em \WINDOWS\system32\drivers\etc..
2. Adicionar Olá após o arquivo de hosts do três entradas tooyour: **endereço IP DATA 0**, **endereço IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.
3. Insira o número de série do dispositivo Olá que você salvou anteriormente. Mapear este endereço IP toohello conforme Olá a imagem a seguir. Para o controlador 0 e 1, acrescente **Controller0** e **Controller1** final Olá Olá do número de série (nome CN).
   
    ![Adicionando nome CN toohosts arquivo](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Salvar arquivo de hosts de saudação.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Conecte o dispositivo de toohello do host remoto Olá

Usar o Windows PowerShell e SSL tooenter uma sessão SSAdmin em seu dispositivo de um host remoto ou cliente. sessão de SSAdmin Olá mapeia toooption 1 no hello [console serial](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.

Execute Olá seguindo o procedimento no computador de saudação do qual você deseja a conexão do toomake Olá remoto do Windows PowerShell.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter uma sessão SSAdmin no dispositivo hello usando o Windows PowerShell e SSL
1. Inicie uma sessão do Windows PowerShell como administrador.
2. Adicione hosts confiáveis do cliente do toohello endereço IP hello dispositivo digitando:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Onde <*device_ip*> é o endereço IP de saudação do seu dispositivo; por exemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. toocreate uma nova credencial, digite:
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Onde <*IP do dispositivo de destino*> é Olá endereço IP de DATA 0 do seu dispositivo; por exemplo, **10.126.173.90** conforme Olá anterior a imagem do arquivo de hosts de saudação. Além disso, forneça a senha do administrador de saudação para seu dispositivo.
4. Crie uma sessão, digitando:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Olá - ComputerName no parâmetro no cmdlet hello, fornecer hello <*número de série do dispositivo de destino*>. Este número de série foi mapeado toohello endereço IP de DATA 0 no arquivo de hosts Olá no seu host remoto. Por exemplo, **SHX0991003G44MT** conforme Olá a imagem a seguir.
5. Tipo:
   
     `Enter-PSSession $session`
6. Você precisará toowait alguns minutos e, em seguida, será conectado tooyour dispositivo via HTTPS sobre SSL. Você verá uma mensagem que indica que você está conectado tooyour dispositivo.
   
    ![PowerShell remoto usando HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [usando o Windows PowerShell tooadminister seu dispositivo StorSimple](storsimple-8000-windows-powershell-administration.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

