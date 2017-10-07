---
title: aaaInstall MongoDB em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB em uma VM do Azure executando o Windows Server 2012 R2 criados com o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Instalar e configurar o MongoDB em uma VM do Windows no Azure
[O MongoDB](http://www.mongodb.org) é um popular banco de dados NoSQL de código-fonte aberto e de alto desempenho. Este artigo lhe orienta pela instalação e configuração do MongoDB em uma VM (máquina virtual) do Windows Server 2012 R2 no Azure. Você também pode [instalar o MongoDB em uma VM do Linux no Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de instalar e configurar o MongoDB, você precisa toocreate uma VM e, idealmente, adicione um tooit de disco de dados. Consulte Olá artigos toocreate uma máquina virtual a seguir e adicione um disco de dados:

* Criar uma VM do Windows Server usando [Olá portal do Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).
* Anexar um dados disco tooa VM do Windows Server usando [Olá portal do Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).

toobegin instalando e configurando o MongoDB, [logon tooyour VM do Windows Server](connect-logon.md) usando a área de trabalho remota.

## <a name="install-mongodb"></a>Instalar o MongoDB
> [!IMPORTANT]
> Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão. Recursos de segurança devem ser habilitados antes de implantar o ambiente de produção do MongoDB tooa. Para obter mais informações, veja [Segurança e Autenticação do MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Depois de conectado tooyour VM usando a área de trabalho remota, abra o Internet Explorer da saudação **iniciar** menu Olá VM.
2. Selecione **usar as configurações de segurança, privacidade e compatibilidade recomendadas** quando o Internet Explorer abrir pela primeira vez e clique em **OK**.
3. A configuração de segurança reforçada do Internet Explorer é habilitada por padrão. Adicione lista de toohello de sites Olá MongoDB de sites permitidos:
   
   * Selecione Olá **ferramentas** ícone no canto superior direito de saudação.
   * Em **opções da Internet**, selecione Olá **segurança** guia e, em seguida, selecione Olá **Sites confiáveis** ícone.
   * Clique em Olá **Sites** botão. Adicionar *https://\*. mongodb.org* toohello lista de sites confiáveis e caixa de diálogo Olá feche.
     
     ![Definir as configurações de segurança do Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Procurar toohello [Downloads do MongoDB -](http://www.mongodb.org/downloads) (http://www.mongodb.org/downloads) da página.
5. Se necessário, selecione Olá **Community Server** edition e, em seguida, selecione Olá versão mais recente atual estável e posterior para Windows Server 2008 R2 de 64 bits. toodownload Olá instalador, clique em **DOWNLOAD (msi)**.
   
    ![Baixar o instalador do MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Execute o instalador de saudação após a conclusão do download de saudação.
6. Leia e aceite o contrato de licença de saudação. Quando solicitado, selecione a instalação **Completa**.
7. Na tela final do hello, clique em **instalar**.

## <a name="configure-hello-vm-and-mongodb"></a>Configurar hello VM e o MongoDB
1. variáveis de caminho Olá não são atualizadas pelo instalador do MongoDB hello. Sem Olá MongoDB `bin` local em sua variável de caminho, você precisa toospecify Olá completo caminho sempre que usar um executável do MongoDB. variável de caminho do tooyour tooadd Olá local:
   
   * Saudação de atalho **iniciar** menu e selecione **sistema**.
   * Clique na guia **Configurações avançadas do sistema** e em **Variáveis de Ambiente**.
   * Em **Variáveis de sistema**, selecione **Caminho** e, em seguida, clique em **Editar**.
     
     ![Configurar variáveis PATH](./media/install-mongodb/configure-path-variables.png)
     
     Adicionar caminho de saudação tooyour MongoDB `bin` pasta. Geralmente, o MongoDB é instalado em *C:\Arquivos de Programas\MongoDB*. Verifique se o caminho de instalação Olá na sua VM. Olá, exemplo a seguir adiciona saudação padrão MongoDB instalação local toohello `PATH` variável:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Ser se tooadd Olá principal-e-vírgula (`;`) tooindicate que você está adicionando um tooyour local `PATH` variável.

2. Crie diretórios de dados e de log do MongoDB no disco de dados. De saudação **iniciar** menu, selecione **Prompt de comando**. Olá exemplos a seguir cria diretórios Olá na unidade f:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Iniciar uma instância do MongoDB com hello comando a seguir, ajustando dados tooyour do caminho do hello e diretórios de log adequadamente:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Pode levar vários minutos para o MongoDB tooallocate arquivos de diário hello e comece a escutar conexões. Todas as mensagens de log são direcionado toohello *F:\MongoLogs\mongolog.log* de arquivos como `mongod.exe` server é iniciado e aloca arquivos de diário.
   
   > [!NOTE]
   > prompt de comando Olá permanece voltada para essa tarefa enquanto a instância do MongoDB está em execução. Deixe Olá prompt de comando janela aberta toocontinue executando o MongoDB. Ou, instale o MongoDB como serviço, conforme detalhado na próxima etapa do hello.

4. Para uma experiência mais robusta do MongoDB, instalar Olá `mongod.exe` como um serviço. Criando um serviço significa que você não precisa tooleave um prompt de comando executando cada vez que você deseja toouse MongoDB. Crie serviço de saudação como a seguir, ajustando os diretórios de dados e log de tooyour de caminho do hello adequadamente:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Olá comando anterior cria um serviço denominado MongoDB, com uma descrição de "Mongo DB". Olá parâmetros a seguir também está especificada:
   
   * Olá `--dbpath` opção especifica o local de saudação do diretório de dados de saudação.
   * Olá `--logpath` opção deve ser usado toospecify um arquivo de log, porque o serviço em execução Olá não tem uma saída toodisplay da janela de comando.
   * Olá `--logappend` opção especifica que uma reinicialização do serviço Olá faz com que o arquivo de log existente do saída tooappend toohello.
   
   serviço de MongoDB em Olá toostart, execute o comando a seguir de saudação:
   
    ```
    net start MongoDB
    ```
   
    Para obter mais informações sobre como criar um serviço do MongoDB hello, consulte [configurar um serviço do Windows para o MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Instância do teste Olá MongoDB
Com o MongoDB em execução como uma única instância ou instalado como um serviço, agora você pode começar a criar e usar seus bancos de dados. Olá toostart shell administrativo do MongoDB, abrir outra janela do prompt de comando do hello **iniciar** menu e digite Olá comando a seguir:

```
mongo  
```

Você pode listar os bancos de dados de saudação com hello `db` comando. Inserir alguns dados da seguinte maneira:

```
db.foo.insert( { a : 1 } )
```

Pesquise por dados da seguinte maneira:

```
db.foo.find()
```

saudação de saída é similar toohello exemplo a seguir:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Saudação de saída `mongo` console da seguinte maneira:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Configurar regras de firewall e de Grupo de Segurança de Rede
Agora que o MongoDB está instalado e em execução, abra uma porta no Firewall do Windows para conectar-se remotamente tooMongoDB. toocreate uma nova regra de entrada tooallow a porta TCP 27017, abra um prompt do PowerShell administrativo e digite Olá comando a seguir:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Você também pode criar regra de saudação usando Olá **Firewall do Windows com segurança avançada** ferramenta de gerenciamento gráfico. Crie uma nova regra de entrada tooallow TCP porta 27017.

Se necessário, crie um grupo de segurança de rede regra tooallow acesso tooMongoDB de fora da sub-rede de rede virtual do Azure existente hello. Você pode criar regras de grupo de segurança de rede de saudação usando Olá [portal do Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md). Assim como acontece com as regras de Firewall do Windows hello, permitir a interface de rede virtual do TCP porta 27017 toohello da VM MongoDB.

> [!NOTE]
> A porta TCP 27017 é saudação padrão usado pelo MongoDB. Você pode alterar essa porta usando Olá `--port` parâmetro ao iniciar `mongod.exe` manualmente ou de um serviço. Se você alterar a porta hello, tornar-se de que tooupdate Olá Firewall do Windows e o grupo de segurança de rede regras em Olá etapas anteriores.


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como tooinstall e configurar o MongoDB em VM do Windows. Agora você pode acessar MongoDB em sua VM do Windows, por seguintes Olá avançado tópicos Olá [documentação do MongoDB](https://docs.mongodb.com/manual/).

