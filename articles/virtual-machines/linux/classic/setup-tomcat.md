---
title: "aaaSet o Apache Tomcat em uma máquina virtual Linux | Microsoft Docs"
description: "Saiba como tooset o Apache Tomcat7 usando máquinas virtuais do Azure executando o Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Configurar o Tomcat7 em uma máquina virtual Linux com o Azure
Apache Tomcat (ou simplesmente Tomcat, também anteriormente denominado Tomcat Jacarta) é um servidor web de código-fonte aberto e o contêiner de servlet desenvolvido pela Olá Apache Software Foundation (ASF). Tomcat implementa hello Servlet Java e especificações de JavaServer Pages (JSP) Olá da Sun Microsystems. Tomcat fornece um ambiente de servidor de web HTTP de Java puro no qual toorun código Java. Configuração mais simples de hello, Tomcat é executado em um processo do sistema operacional. Esse processo é executado em uma máquina virtual Java (JVM). Todas as solicitações HTTP de um navegador tooTomcat é processada como um thread separado no processo de saudação do Tomcat.  

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda como toouse Olá modelo de implantação clássico. É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. toouse um modelo de Gerenciador de recursos toodeploy uma VM Ubuntu com Open JDK e o Tomcat, consulte [neste artigo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

Neste artigo, você instalará o Tomcat7 em uma imagem do Linux e a implantará no Azure.  

Você aprenderá:  

* Como toocreate uma máquina virtual no Azure.
* Como tooprepare hello máquina virtual para Tomcat7.
* Como tooinstall Tomcat7.

Supomos que você já tem uma assinatura do Azure.  Se não, você pode se inscrever para uma avaliação gratuita em [Olá site do Azure](https://azure.microsoft.com/). Se você tiver uma assinatura do MSDN, confira [Preço especial do Microsoft Azure: benefícios do MSDN, MPN e BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn mais sobre o Azure, consulte [o que é o Azure?](https://azure.microsoft.com/overview/what-is-azure/).

Este artigo pressupõe que você tenha conhecimento prático básico do Tomcat e Linux.  

## <a name="phase-1-create-an-image"></a>Fase 1: Criar uma imagem
Nesta fase, você criará uma máquina virtual usando uma imagem do Linux no Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Etapa 1: Gerar uma chave de autenticação SSH
O SSH é uma ferramenta importante para os administradores do sistema. No entanto, não é recomendado configurar a segurança de acesso com base em uma senha determinada por humanos. Usuários mal-intencionados podem entrar em seu sistema usando um nome de usuário e uma senha fraca.

Olá boa notícia é que há uma maneira de acesso remoto tooleave abrir e não se preocupar com senhas. O método consiste na autenticação com criptografia assimétrica. Olá, chave privada do usuário é hello que concede a autenticação de saudação. Você pode até mesmo bloquear Olá conta de usuário toonot permitir a autenticação de senha.

Outra vantagem desse método é que você não precisa toosign senhas diferentes em servidores toodifferent. Você pode autenticar usando Olá pessoal chave privada em todos os servidores, que impede que você tenha tooremember várias senhas.



Siga estas etapas toogenerate Olá SSH da chave de autenticação.

1. Baixe e instale o PuTTYgen da saudação local a seguir: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Execute o Puttygen.exe.
3. Clique em **gerar** toogenerate chaves de saudação. No processo de saudação, você pode aumentar aleatoriedade pela movimentação do mouse Olá sobre a área em branco Olá na janela de saudação.  
   ![Captura de tela de gerador de chave puTTY que mostra Olá gerar novo botão de chave][1]
4. Depois de saudação Gerar processo, Puttygen.exe mostrará sua nova chave pública.  
   ![Captura de tela de gerador de chave puTTY que mostra a nova chave pública de saudação e hello Salvar botão da chave privada][2]
5. Selecione e copie a chave pública hello e salvá-lo em um arquivo chamado publicKey.pem. Não clique **salva a chave pública**, pois Olá salvo o formato de arquivo da chave pública é diferente da chave pública de saudação que desejamos.
6. Clique em **Salvar chave privada** e salve-a em um arquivo chamado privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Etapa 2: Criar a imagem de saudação em Olá portal do Azure
1. Em Olá [portal](https://portal.azure.com/), clique em **novo** em Olá barra de tarefas toocreate uma imagem. Escolha Olá Linux imagem com base em suas necessidades. Olá, exemplo a seguir usa Olá Ubuntu 14.04 imagem.
![Captura de tela de portal Olá que mostra o botão novo Olá][3]

2. Para **nome de Host**, especifique nome Olá Olá URL que você e os clientes da Internet usará tooaccess esta máquina virtual. Defina a última parte Olá de nome DNS hello, por exemplo, tomcatdemo. Azure gera Olá URL como tomcatdemo.cloudapp.net.  

3. Para **chave de autenticação SSH**, copie o valor de chave de saudação do arquivo de publicKey.pem hello, que contém chave pública de saudação gerado pelo PuTTYgen.  
![Caixa de chave de autenticação SSH no portal de saudação][4]

4. Defina as outras configurações conforme necessário e, em seguida, clique em **Criar**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Fase 2: Preparar sua máquina virtual para o Tomcat7
Nesta fase, você configurar um ponto de extremidade para o tráfego do Tomcat e, em seguida, conecte-se tooyour nova máquina de virtual.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Etapa 1: Abrir o acesso via web do hello HTTP porta tooallow
Os pontos de extremidade no Azure são compostos por um protocolo TCP ou UDP juntamente com uma porta pública e privada. Olá privada porta é Olá que serviço Olá escutando tooon Olá VM. porta pública Olá é a porta Olá Olá serviço de nuvem do Azure escuta tooexternally para o tráfego de entrada, baseado na Internet.  

A porta TCP 8080 é o número da porta padrão Olá Tomcat usa toolisten. Se esta porta for aberta com um Ponto de Extremidade do Azure, você e outros clientes da Internet poderão acessar páginas do Tomcat.  

1. No portal de saudação, clique em **procurar** > **máquinas virtuais**e, em seguida, clique em máquina virtual Olá que você criou.  
   ![Captura de tela de diretório do hello máquinas virtuais][5]
2. tooadd uma máquina virtual de tooyour de ponto de extremidade, clique em Olá **pontos de extremidade** caixa.
   ![Captura de tela que mostra a caixa de pontos de extremidade Olá][6]
3. Clique em **Adicionar**.  

   1. Ponto de extremidade hello, insira um nome para o ponto de extremidade de saudação em **ponto de extremidade**e, em seguida, digite 80 na **porta pública**.  

      Se você definir too80, número da porta tooinclude Olá Olá URL que é usado tooaccess Tomcat não é necessário. Por exemplo, http://tomcatdemo.cloudapp.net.    

      Se você definir o valor de tooanother, como 81, será necessário tooadd Olá porta número toohello URL tooaccess Tomcat. Por exemplo, http://tomcatdemo.cloudapp.net:81/.
   2. Digite 8080 em **Porta Privada**. Por padrão, o Tomcat escuta a porta 8080 TCP. Se você alterou a porta de escuta de padrão saudação do Tomcat, você deve atualizar **porta privada** toobe Olá mesmo Olá porta de escuta do Tomcat.  
      ![Captura de tela da interface do usuário que mostra o comando Adicionar, a Porta Pública e a Porta Privada][7]
4. Clique em **Okey** tooadd Olá ponto de extremidade tooyour VM.

### <a name="step-2-connect-toohello-image-you-created"></a>Etapa 2: Conectar-se a imagem toohello criada
Você pode escolher qualquer máquina virtual do SSH ferramenta tooconnect tooyour. Neste exemplo, usamos PuTTY.  

1. Obter nome DNS de saudação de sua máquina virtual no portal de saudação.
    1. Clique em **Procurar** > **Máquinas Virtuais**.
    2. Selecione Olá nome da máquina virtual e, em seguida, clique em **propriedades**.
    3. Em Olá **propriedades** lado a lado, procure em Olá **nome de domínio** nome DNS do caixa tooget hello.  

2. Obter o número da porta Olá para conexões SSH de saudação **SSH** caixa.  
![Captura de tela que mostra o número da porta de conexão do hello SSH][8]

3. Baixe [PuTTY](http://www.putty.org/).  

4. Após o download, clique em arquivo executável do hello Putty.exe. Configuração PuTTY, configurar opções básicas de saudação com o nome de host de saudação e porta número que é obtido das propriedades de saudação de sua máquina virtual.   
![Captura de tela que mostra as opções de nome e a porta de host de configuração PuTTY Olá][9]

5. No painel esquerdo do hello, clique em **Conexão** > **SSH** > **Auth**e, em seguida, clique em **procurar** toospecify local de saudação do arquivo de privateKey.ppk de saudação. arquivo de privateKey.ppk de Olá contém a chave privada de saudação que é gerado pelo PuTTYgen anteriormente hello "Fase 1: criar uma imagem" deste artigo.  
![Captura de tela que mostra a hierarquia de diretórios de Conexão hello e o botão Procurar][10]

6. Clique em **Abrir**. Você pode ser alertado por uma caixa de mensagem. Se você tiver configurado o nome DNS hello e número da porta corretamente, clique em **Sim**.
![Captura de tela que mostra a notificação de saudação][11]

7. Você está tooenter solicitado seu nome de usuário.  
![Captura de tela que mostra onde username tooenter][12]

8. Insira nome de usuário de saudação que você usou toocreate Olá VM em hello "Fase 1: criar uma imagem" seção neste artigo. Você verá algo parecido com hello seguinte:  
![Captura de tela que mostra a confirmação de autenticação Olá][13]

## <a name="phase-3-install-software"></a>Fase 3: Instalar o software
Nesta fase, você pode instalar o Java runtime environment hello, Tomcat7 e outros componentes de Tomcat7.  

### <a name="java-runtime-environment"></a>Java runtime environment
O tomcat é escrito em Java. Há dois tipos de JDKs (Kits de desenvolvimento Java), OpenJDK e Oracle JDK. Você pode escolher Olá aquele que você deseja.  

> [!NOTE]
> Tanto JDKs tem quase Olá mesmo código para classes Olá Olá API Java, mas Olá código para a máquina virtual de saudação é diferente. OpenJDK tende a bibliotecas abertas toouse, enquanto tende a Oracle JDK toouse fechado aqueles. O Oracle JDK tem mais classes e alguns bugs corrigidos, sendo também mais estável que o OpenJDK.

#### <a name="install-openjdk"></a>Instalar o OpenJDK  

Use Olá toodownload comando OpenJDK a seguir.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate toocontain um diretório Olá arquivos JDK:  

        sudo mkdir /usr/lib/jvm  
* arquivos JDK tooextract Olá no diretório usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Instalar o Oracle JDK


Use Olá toodownload comando Oracle JDK a seguir no site da Oracle de saudação.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate toocontain um diretório Olá arquivos JDK:  

        sudo mkdir /usr/lib/jvm  
* arquivos JDK tooextract Olá no diretório usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset Oracle JDK como Olá a máquina virtual Java com padrão:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Confirme se a instalação do Java foi bem-sucedida
Você pode usar um comando como Olá tootest a seguir se Olá Java runtime environment está instalado corretamente:  

    java -version  

Se você instalou OpenJDK, você verá uma mensagem semelhante seguinte Olá: ![mensagem de instalação OpenJDK bem-sucedida][14]

Se você instalou o JDK da Oracle, você verá uma mensagem semelhante seguinte Olá: ![mensagem de instalação do JDK bem-sucedida do Oracle][15]

### <a name="install-tomcat7"></a>Instalar o Tomcat7
Use Olá comando tooinstall Tomcat7 a seguir.  

    sudo apt-get install tomcat7  

Se você não estiver usando Tomcat7, use a variação apropriada Olá desse comando.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Confirme se a instalação do Tomcat7 foi bem-sucedida
toocheck se Tomcat7 for instalado com êxito, procure o nome DNS do servidor do tooyour Tomcat. Neste artigo, URL de exemplo hello é http://tomcatexample.cloudapp.net/. Se você vir uma mensagem semelhante Olá seguinte, Tomcat7 está instalado corretamente.
![Mensagem de instalação bem-sucedida do Tomcat7][16]

### <a name="install-other-tomcat7-components"></a>Instalar outros componentes do Tomcat7
Há outros componentes opcionais do Tomcat que você pode instalar.  

Saudação de uso **tomcat7 de pesquisa de cache apt sudo** toosee comando todos os componentes disponíveis hello. Use Olá tooinstall comandos a seguir alguns componentes úteis.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Fase 4: Configurar o Tomcat7
Nesta fase, você administrará o Tomcat.

### <a name="start-and-stop-tomcat7"></a>Iniciar e parar o Tomcat7
servidor de Tomcat7 Olá é iniciado automaticamente quando você instalá-lo. Você também poderá iniciá-lo com hello comando a seguir:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

status de saudação do tooview do Tomcat7:

    sudo /etc/init.d/tomcat7 status

serviços do Tomcat toorestart: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Administração do Tomcat7
Você pode editar tooset de arquivo de configuração do hello Tomcat usuário se suas credenciais de administrador. Use Olá comando a seguir:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Aqui está um exemplo:  
![Captura de tela que mostra a saída do comando Olá sudo vi][17]  

> [!NOTE]
> Crie uma senha forte para o nome de usuário de administrador hello.  

Depois de editar esse arquivo, é necessário reiniciar os serviços de Tomcat7 com hello tooensure de comando que Olá alterações entrem em vigor a seguir:  

    sudo /etc/init.d/tomcat7 restart  

Abra seu navegador e digite **http://<your tomcat server DNS name>manager/html** como Olá URL. Por exemplo hello neste artigo, URL Olá é http://tomcatexample.cloudapp.net/manager/html.  

Depois de se conectar, você verá algo semelhante seguinte de toohello:  
![Captura de tela da saudação Gerenciador de aplicativos da Web Tomcat][18]

## <a name="common-issues"></a>Problemas comuns
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Não é possível acessar a máquina virtual Olá Tomcat e o Moodle de saudação da Internet
#### <a name="symptom"></a>Sintoma  
  Tomcat está sendo executado, mas você não conseguir ver a página de padrão do Tomcat Olá com seu navegador.
#### <a name="possible-root-cause"></a>Possível causa raiz   

  * porta de escuta do Tomcat Olá não é Olá mesmo que a porta privada saudação do ponto de extremidade da sua máquina virtual para o tráfego do Tomcat.  

     Verifique a porta pública e privada configurações de ponto de extremidade de porta e verifique se a porta privada Olá é Olá mesmo Olá Tomcat a porta de escuta. Consulte a seção “Fase 1: Criar uma imagem” deste artigo para obter instruções sobre como configurar os pontos de extremidade para sua máquina virtual.  

     Olá toodetermine Tomcat porta de escuta, abra /etc/httpd/conf/httpd.conf (versão do Red Hat) ou /etc/tomcat7/server.xml (versão Debian). Por padrão, a saudação porta de escuta do Tomcat é 8080. Aqui está um exemplo:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Se você estiver usando uma máquina virtual que Debian ou Ubuntu e você deseja toochange saudação padrão porta do Tomcat escutar (por exemplo, 8081), você também deve abrir a porta Olá para o sistema operacional de saudação. Primeiro, abra o perfil de saudação:  

        sudo vi /etc/default/tomcat7  

     Em seguida, remova a última linha de saudação e altere "não" muito "Sim".  

        AUTHBIND=yes
  2. firewall Olá desabilitou Olá porta de escuta do Tomcat.

     Você só pode ver a página do hello Tomcat padrão do host local hello. problema de saudação é mais provável que porta hello, que é atendida tooby Tomcat, seja bloqueada pelo firewall hello. Você pode usar a página da Web do hello w3m ferramenta toobrowse hello. Olá comandos a seguir instalar w3m e procurar toohello Tomcat padrão página:  


        sudo yum  install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>Solução

  * Se Olá porta de escuta do Tomcat não está hello mesmo como a porta privada saudação do ponto de extremidade de saudação da máquina de virtual toohello tráfego, você precisará alterá porta privada Olá toobe Olá mesmo Olá porta de escuta do Tomcat.   
  2. Se Olá problema é causado por um firewall/iptables, adicione Olá linhas muito/etc/sysconfig/iptables a seguir. segunda linha de saudação é necessário apenas para tráfego https:  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > Certifique-se de linhas anteriores Olá são posicionadas acima todas as linhas que globalmente seriam restringir o acesso, como a seguir Olá: - A -j rejeitar – rejeitar com proibido de host de icmp de entrada



iptables tooreload hello, executar Olá comando a seguir:

    service iptables restart

Isso foi testado no CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Permissão negada ao carregar projeto arquivos muito/var/lib/tomcat7/webapps /
#### <a name="symptom"></a>Sintoma
  Quando você usar uma máquina virtual do SFTP cliente (como FileZilla) tooconnect tooyour e navegue muito/var/lib/tomcat7/webapps/toopublish seu site, você obtém uma erro mensagem semelhante toohello a seguir:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Possível causa raiz
  Você não tem nenhuma pasta de /var/lib/tomcat7/webapps permissões tooaccess hello.  
#### <a name="solution"></a>Solução  
  Você precisa de permissão de tooget da conta raiz de saudação. Você pode alterar a propriedade Olá dessa pasta de raiz toohello nome de usuário usado ao provisionar a máquina de saudação. Aqui está um exemplo com o nome da conta azureuser hello:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Use permissões de Olá Olá -R opção tooapply para todos os arquivos dentro de um diretório também.  

  Este comando também funciona para diretórios. as alterações da opção -R Olá Olá permissões para todos os arquivos e diretórios dentro do diretório de saudação. Aqui está um exemplo:  

     sudo chown -R username:group directory  

  Esse comando altera a propriedade (usuário e grupo) para todos os arquivos e pastas que estão dentro do diretório de saudação.  

  Olá comando a seguir altera somente permissão de saudação do diretório da pasta hello. arquivos de saudação e pastas dentro do diretório de saudação não são alteradas.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
