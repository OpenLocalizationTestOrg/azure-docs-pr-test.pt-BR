## <a name="prepare-your-raspberry-pi"></a>Preparar seu Raspberry Pi

### <a name="install-raspbian"></a>Instalar Raspbian

Se isso for Olá primeira vez que você estiver usando o Pi framboesa, é necessário tooinstall Olá Raspbian o sistema operacional usando NOOBS no cartão SD de saudação incluído no kit de saudação. Olá [framboesa Pi Software guia] [ lnk-install-raspbian] descreve como tooinstall um sistema operacional em seu framboesa Pi. Este tutorial presume que você instalou o sistema de operacional Raspbian Olá no seu framboesa Pi.

> [!NOTE]
> cartão de saudação SD incluído no hello [Microsoft Azure IoT Starter Kit para framboesa Pi 3] [ lnk-starter-kits] já tem NOOBS instalado. Pode ser inicializado Olá framboesa Pi neste cartão e escolha tooinstall Olá Raspbian SO.

configuração de hardware do toocomplete hello, você precisa:

- Conecte-se a fonte de alimentação toohello framboesa Pi incluída no kit de saudação.
- Conecte a sua rede de tooyour framboesa Pi usando cabo Ethernet de saudação incluído no kit. Como alternativa, você pode configurar [Conectividade sem fio][lnk-pi-wireless] para o Raspberry Pi.

Agora você concluiu a instalação de hardware Olá de seu Pi framboesa.

### <a name="sign-in-and-access-hello-terminal"></a>Entrar e acessar terminal Olá

Você tem um ambiente de terminal tooaccess de duas opções com seu Pi framboesa:

- Se você tiver um teclado e monitorar tooyour conectado framboesa Pi, você pode usar o hello GUI Raspbian tooaccess uma janela de terminal.

- Acesso a linha de comando do hello no seu Pi framboesa usando SSH em seu computador desktop.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Use uma janela de terminal Olá GUI

credenciais de padrão de saudação para Raspbian são o nome de usuário **pi** e a senha **framboesa**. Na barra de tarefas de saudação em Olá GUI, você pode iniciar Olá **Terminal** utilitário usando o ícone de saudação que se parece com um monitor.

#### <a name="sign-in-with-ssh"></a>Entre com o SSH

Você pode usar o SSH para acesso de linha de comando tooyour framboesa Pi. artigo Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH com o Pi framboesa e como tooconnect de [Windows] [ lnk-ssh-windows] ou [Sistema operacional Linux e Mac][lnk-ssh-linux].

Entre com o nome de usuário **pi** e a senha **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Opcional: Compartilhar uma pasta em seu Raspberry Pi

Opcionalmente, talvez você queira tooshare uma pasta no seu Pi framboesa com seu ambiente de área de trabalho. Uma pasta de compartilhamento permite que você toouse seu editor de texto preferido de área de trabalho (como [código do Visual Studio](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit arquivos em seu Pi framboesa em vez de usar `nano` ou `vi`.

tooshare uma pasta com o Windows, configure um servidor do Samba no hello framboesa Pi. Como alternativa, usar interno de saudação [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server com um cliente SFTP na área de trabalho.

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/