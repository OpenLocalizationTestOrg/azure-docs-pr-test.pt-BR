## <a name="prepare-your-intel-nuc"></a>Preparar o Intel NUC

configuração de hardware do toocomplete hello, você precisa:

- Conecte-se a fonte de alimentação Intel NUC toohello incluída no kit de saudação.
- Conecte-se a rede de tooyour Intel NUC usando um cabo Ethernet.

Você acabou de concluir instalação de hardware de saudação do seu dispositivo de gateway NUC Intel.

### <a name="sign-in-and-access-hello-terminal"></a>Entrar e acessar terminal Olá

Você tem um ambiente de terminal tooaccess de duas opções no seu NUC Intel:

- Se você tiver um teclado e monitorar conectado tooyour NUC Intel, você pode acessar diretamente o shell hello. as credenciais padrão Olá são username **raiz** e a senha **raiz**.

- Shell de saudação de acesso no seu NUC Intel usando SSH em seu computador desktop.

#### <a name="sign-in-with-ssh"></a>Entre com o SSH

toosign com SSH, é necessário o endereço IP de saudação do seu NUC Intel. Se você tiver um teclado e monitorar conectado tooyour NUC Intel, use Olá `ifconfig` toofind endereço IP de saudação do comando. Como alternativa, conecte-se a endereços de saudação do tooyour roteador toolist de dispositivos na sua rede.

Entre com o nome de usuário **raiz** e a senha **raiz**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Opcional: Compartilhar uma pasta em seu Intel NUC

Opcionalmente, talvez você queira tooshare uma pasta no seu NUC Intel com seu ambiente de área de trabalho. Uma pasta de compartilhamento permite que você toouse seu editor de texto preferido de área de trabalho (como [código do Visual Studio](https://code.visualstudio.com/) ou [texto Sublime](http://www.sublimetext.com/)) tooedit arquivos em seu NUC Intel, em vez de usar `nano` ou `vi`.

tooshare uma pasta com o Windows, configure um servidor do Samba no hello NUC Intel. Como alternativa, use servidor SFTP Olá em Olá Intel NUC com um cliente SFTP em seu computador desktop.
