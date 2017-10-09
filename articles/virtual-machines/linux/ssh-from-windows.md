---
title: chaves de aaaUse SSH com o Windows para VMs do Linux | Microsoft Docs
description: "Saiba como toogenerate e usar SSH de chaves em uma máquina de virtual do Windows computador tooconnect tooa Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Como chaves de tooUse SSH com o Windows no Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Quando você se conectar tooLinux (máquinas virtuais) no Azure, você deve usar [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide um toolog de maneira mais segura em tooyour VM do Linux. Esse processo envolve uma troca de chaves pública e privada usando Olá SSH (secure shell) comando tooauthenticate em vez de um nome de usuário e senha. As senhas são vulneráveis toobrute ataques, especialmente em VMs com a Internet, como servidores web. Este artigo fornece uma visão geral das chaves de SSH como toogenerate Olá chaves apropriadas em um computador com Windows.

## <a name="overview-of-ssh-and-keys"></a>Visão geral do SSH e das chaves
Você pode fazer logon com segurança no tooyour VM Linux usando as chaves públicas e privadas:

* Olá **chave pública** é colocado em sua VM do Linux ou qualquer outro serviço que você deseja toouse com criptografia de chave pública.
* Olá **chave privada** que você está presente tooyour VM Linux quando você fizer logon, tooverify sua identidade. Proteja essa chave privada. Não a compartilhe.

Essas chaves públicas e privadas podem ser usadas em vários serviços e VMs. Não é necessário um par de chaves para cada VM ou serviço que você deseja tooaccess. Para obter uma visão mais detalhada, confira [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography).

O SSH é um protocolo de conexão criptografada que permite logons seguros por conexões não protegidas. É o protocolo de conexão padrão Olá para VMs do Linux hospedado no Azure. Embora SSH próprio fornece uma conexão criptografada, usando senhas com conexões SSH ainda deixa Olá VM vulnerável toobrute ataques ou adivinhação de senhas. Um método mais seguro e preferencial de conexão tooa VM usando o SSH está usando essas chaves públicas e privadas, também conhecido como chaves SSH.

Se você não desejar que as chaves de SSH toouse, você ainda pode fazer logon no tooyour VMs do Linux usando uma senha. Se sua VM não estiver toohello exposto à Internet, usar as senhas pode ser suficiente. No entanto, ainda precisar toomanage suas senhas para cada VM do Linux e manter políticas de senha íntegro e práticas recomendadas, como comprimento mínimo da senha e atualizá-las regularmente. use Olá de chaves SSH reduz a complexidade de saudação do gerenciamento de credenciais individuais em várias VMs.

## <a name="windows-packages-and-ssh-clients"></a>Pacotes do Windows e clientes SSH
Conecte-se tooand gerenciar VMs do Linux no Azure usando um **cliente SSH**. Os computadores Windows geralmente não têm um cliente SSH instalado. saudação de atualização de aniversário do Windows 10 adicionado Bash para Windows e mais recente atualização do Windows 10 criadores hello fornece atualizações adicionais. Este subsistema Windows para Linux permite utilitários toorun e acesso como um cliente SSH nativamente dentro de um shell Bash. Você pode seguir qualquer um dos documentos do Linux hello, tais como [como pares de chave SSH toogenerate para Linux](mac-create-ssh-keys.md). O Bash para Windows ainda está em desenvolvimento e é considerado uma versão beta. Para saber mais sobre o Bash para Windows, confira [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about) (Bash no Ubuntu no Windows).

Se você quiser toouse algo diferente de Bash para Windows, estão incluídos comuns Windows SSH clientes que você pode instalar Olá pacotes a seguir:

* [Git for Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Arquivos de chave que você precisa toocreate?
O Azure requer chaves públicas e privadas de pelo menos 2048 bits em formato **ssh-rsa**. Se você estiver gerenciando recursos do Azure usando o modelo de implantação clássico hello, você também precisa toogenerate um PEM (`.pem` arquivo).

Aqui estão os cenários de implantação hello e tipos de saudação de arquivos que você usa em cada:

1. **SSH-rsa** chaves são necessárias para qualquer implantação usando Olá [portal do Azure](https://portal.azure.com)e as implantações do Gerenciador de recursos usando Olá [CLI do Azure](../../cli-install-nodejs.md).
   * Geralmente, essas chaves são tudo do que a maioria das pessoas precisa.
2. Um `.pem` arquivo é necessário toocreate VMs usando Olá clássico implantação. Essas chaves são suportadas em implantações clássico ao usar Olá [portal do Azure](https://portal.azure.com) ou [CLI do Azure](../../cli-install-nodejs.md).
   * Você só precisa toocreate essas outras chaves e certificados se você estiver gerenciando recursos criados usando o modelo de implantação clássico hello.

## <a name="install-git-for-windows"></a>Instalar o Git for Windows
seção anterior Hello listados vários pacotes que incluem hello `openssl` ferramenta para Windows. Essa ferramenta é que as chaves públicas e privadas toocreate necessários. Olá detalhes de exemplos a seguir como tooinstall e usar **Git para Windows**, embora você pode escolher qualquer pacote que você preferir. **Git para Windows** oferece acesso toosome software de código-fonte aberto adicional ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) ferramentas e utilitários que podem ser úteis ao trabalhar com VMs do Linux.

1. Baixe e instale o **Git para Windows** de saudação local a seguir: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Aceitar opções padrão de saudação durante a saudação processo de instalação, a menos que seja absolutamente necessário toochange-los.
3. Executar **Git Bash** de saudação **Menu Iniciar** > **Git** > **Git Bash**. console de saudação parece semelhante toohello exemplo a seguir:

    ![Shell do Bash do Git para Windows](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Criar uma chave privada
1. No seu **Git Bash** janela, use `openssl.exe` toocreate uma chave privada. Olá, exemplo a seguir cria uma chave chamada `myPrivateKey` e certificado denominado `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    saída de Hello parece semelhante toohello exemplo a seguir:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Se o bash relatar um erro, tente abrir uma nova janela de **Bash do Git** com privilégios elevados. Em seguida, execute novamente a saudação `openssl` comando.

2. Saudação de resposta solicita o nome de país, local, nome da organização, etc.
3. A chave e o certificado novos são criados no diretório atual de trabalho. Como medida de segurança, você deve definir as permissões de saudação em sua chave privada para que somente você pode acessá-lo:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Olá [próxima seção](#create-a-private-key-for-putty) detalhes usando PuTTYgen tooboth exibir e usar a chave pública hello e criar uma chave privada específicos para usar PuTTY tooSSH tooLinux VMs. comando a seguir Hello gera um arquivo de chave pública denominado `myPublicKey.key` que você pode usar imediatamente:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Se você precisar de recursos de clássico toomanage também, converter Olá `myCert.pem` muito`myCert.cer` (X509 codificado em DER certificado). Executar esta etapa opcional somente se você precisar toospecifically gerenciar recursos de clássico mais antigos.

    Converta o certificado de saudação usando Olá comando a seguir:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Criar uma chave privada para PuTTY
O PuTTY é um cliente SSH comum do Windows. Você está livre toouse qualquer cliente SSH que desejar. toouse PuTTY, você precisa toocreate um tipo de chave - uma chave privada de PuTTY (PPK) adicional. Se você não desejar toouse PuTTY, ignore esta seção.

Olá, exemplo a seguir cria essa chave privada adicional especificamente para toouse PuTTY:

1. Use **Git Bash** tooconvert seu privada da chave em uma chave privada do RSA que PuTTYgen pode entender. Olá, exemplo a seguir cria uma chave chamada `myPrivateKey_rsa` da chave existente de saudação chamado `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Como medida de segurança, você deve definir as permissões de saudação em sua chave privada para que somente você pode acessá-lo:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Baixar e executar PuTTYgen Olá local a seguir: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Clique em menu Olá: **arquivo** > **chave privada de carga**
4. Localize sua chave privada (`myPrivateKey_rsa` no exemplo anterior de saudação). diretório padrão de Hello quando você iniciar **Git Bash** é `C:\Users\%username%`. Alterar tooshow de filtro de arquivo hello **todos os arquivos (\*.\*)** :

    ![Carregar a chave privada existente de saudação em PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Clique em **Abrir**. Um prompt indica que essa chave Olá foi importado com êxito:

    ![Chave tooPuTTYgen foram importados com êxito](./media/ssh-from-windows/successfully-imported-key.png)
6. Clique em **Okey** tooclose prompt de saudação.
7. chave pública Olá é exibido na parte superior de saudação do hello **PuTTYgen** janela. Copie e cole essa chave pública Olá portal do Azure ou o modelo do Gerenciador de recursos do Azure quando você criar uma VM do Linux. Você também pode clicar em **salva a chave pública** toosave um computador tooyour de cópia:

    ![Salvar o arquivo de chave pública PuTTY](./media/ssh-from-windows/save-public-key.png)

    Olá exemplo a seguir mostra como você copie e cole essa chave pública a saudação portal do Azure quando você criar uma VM do Linux. chave pública Olá normalmente é armazenado no `~/.ssh/authorized_keys` em sua nova VM.

    ![Use a chave pública quando você cria uma máquina virtual no hello portal do Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. De volta ao **PuTTYgen**, clique em **Salvar chave privada**:

    ![Salvar o arquivo de chave privada PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Um prompt solicita se você deseja toocontinue sem inserir uma senha para a sua chave. Uma frase secreta é como uma chave privada de tooyour anexado de senha. Mesmo se alguém tooobtain sua chave privada, eles ainda não seria capaz de tooauthenticate usando apenas a chave de saudação. Também precisam Olá senha. Sem uma senha, se alguém obtiver sua chave privada, que possam fazer logon no tooany VM ou serviço que usa essa chave. É recomendável criar uma frase secreta. No entanto, não se você esquecer a senha de hello, há nenhuma maneira toorecovê-lo.
   >
   >

    Se você desejar tooenter uma senha, clique em **não**, insira uma senha na janela principal de PuTTYgen hello e, em seguida, clique em **salva a chave privada** novamente. Caso contrário, clique em **Sim** toocontinue sem fornecer a senha opcional hello.
9. Insira um nome e local toosave seu arquivo PPK.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Usar Putty tooSSH tooa computador Linux
Repetindo, PuTTY é um cliente de SSH comum do Windows. Você está livre toouse qualquer cliente SSH que desejar. Olá detalhes de etapas a seguir como toouse seu tooauthenticate chave privada com sua VM do Azure usando o SSH. etapas de saudação são semelhantes em outros clientes de chave SSH em termos de necessidade tooload seu Olá tooauthenticate chave privada conexão SSH.

1. Download e execução putty do hello seguinte local: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Preencha o nome de host de saudação ou endereço IP da VM de saudação portal do Azure:

    ![Abrir nova conexão PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Antes de selecionar **Abrir**, clique em **Conexão** > **SSH** > **guia Autenticação**. Procurar tooand selecione sua chave privada:

    ![Selecionar a Chave Privada PuTTY para autenticação](./media/ssh-from-windows/putty-auth-dialog.png)
4. Clique em **abrir** tooconnect tooyour virtual machine

## <a name="next-steps"></a>Próximas etapas
Você também pode gerar as chaves públicas e privadas Olá [usando OS X e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para obter mais informações sobre Bash para Windows e os benefícios de saudação de ter as ferramentas de OSS prontamente disponíveis no seu computador Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).

Se você tiver problemas ao usar SSH tooconnect tooyour VMs do Linux, consulte [solucionar problemas de SSH conexões tooan VM do Linux Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
