---
title: aaaSet backup PostgreSQL em uma VM do Linux | Microsoft Docs
description: "Saiba como tooinstall e configurar PostgreSQL em uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Instalar e configurar o PostgreSQL no Azure
PostgreSQL é tooOracle semelhante de banco de dados avançado do código-fonte aberto e DB2. Ele inclui recursos corporativos como conformidade total com ACID, processamento transacional confiável e controle de simultaneidade de várias versões. Também oferece suporte a padrões como ANSI SQL e SQL/MED (inclusive wrappers de dados externos para Oracle, MySQL, MongoDB e muitos outros). Ele é altamente extensível com suporte para mais de 12 idiomas de procedimento, índices GIN e GiST, dados espaciais e vários recursos como NoSQL para aplicativos JSON ou de chave-valor.

Neste artigo, você aprenderá como tooinstall e configurar PostgreSQL em uma máquina virtual do Azure executando o Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Instalar o PostgreSQL
> [!NOTE]
> Você já deve ter uma máquina virtual do Azure executando o Linux em ordem toocomplete neste tutorial. toocreate e configurar uma VM do Linux antes de continuar, consulte o [tutorial de VM do Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

Nesse caso, use a porta 1999 como Olá PostgreSQL porta.  

Conecte-se toohello VM do Linux criado por meio do PuTTY. Se este for Olá pela primeira vez que você está usando uma VM do Linux do Azure, consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn como toouse PuTTY tooconnect tooa VM do Linux.

1. Comando a seguir de execução Olá tooswitch toohello raiz (administrador):
   
        # sudo su -
2. Algumas distribuições têm dependências que devem ser instaladas antes de instalar o PostgreSQL. Verifique a distribuição da lista e execute o comando apropriado hello:
   
   * Linux baseado em Red Hat:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Linux baseado em Debian:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Baixar PostgreSQL no diretório raiz de saudação e, em seguida, descompacte o pacote de saudação:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Olá acima é um exemplo. Você pode encontrar hello mais detalhado baixar endereço no hello [índice de /pubfonte/](https://ftp.postgresql.org/pub/source/).
4. compilação toostart hello, execute estes comandos:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Se você quiser toobuild tudo o que pode ser criado, incluindo documentação hello (páginas HTML e man) e módulos adicionais (Contribuidor), execute Olá comando a seguir em vez disso:
   
        # gmake install-world
   
    Você deve receber Olá a seguinte mensagem de confirmação:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Configurar PostgreSQL
1. (Opcional) Criar uma saudação do link simbólico tooshorten PostgreSQL referência toonot incluem o número de versão de hello:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Crie um diretório para o banco de dados de saudação:
   
        # mkdir -p /opt/pgsql_data
3. Crie um usuário não raiz e modifique o perfil do usuário. Em seguida, alternar toothis novo usuário (chamado *postgres* em nosso exemplo):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Por motivos de segurança, PostgreSQL usa tooinitialize um usuário não raiz, iniciar ou encerrar Olá banco de dados.
   > 
   > 
4. Editar saudação *bash_profile* arquivo digitando comandos de saudação abaixo. Essas linhas serão adicionadas toohello final de saudação *bash_profile* arquivo:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Executar Olá *bash_profile* arquivo:
   
        $ source .bash_profile
6. Valide a instalação usando o comando a seguir de saudação:
   
        $ which psql
   
    Se a instalação for bem-sucedida, você verá Olá resposta a seguir:
   
        /opt/pgsql/bin/psql
7. Você também pode verificar a versão de PostgreSQL hello:
   
        $ psql -V
8. Inicialize o banco de dados de saudação:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Você deve receber Olá saída a seguir:

![imagem](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Configurar o PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Execute Olá comandos a seguir:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Modificar as duas variáveis no arquivo de /etc/init.d/postgresql hello. Olá é definido toohello caminho de instalação do PostgreSQL: **/opt/pgsql**. PGDATA é definir o caminho de armazenamento de dados toohello de PostgreSQL: **/opt/pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![imagem](./media/postgresql-install/no2.png)

Alterar Olá arquivo toomake-executável:

    # chmod +x /etc/init.d/postgresql

Inicie o PostgreSQL:

    # /etc/init.d/postgresql start

Verifique se o ponto de extremidade de saudação do PostgreSQL está em:

    # netstat -tunlp|grep 1999

Você deve ver Olá saída a seguir:

![imagem](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Conecte-se o banco de dados do toohello Postgres
Alterne toohello postgres usuário novamente:

    # su - postgres

Crie um banco de dados Postgres:

    $ createdb events

Conecte-se o banco de dados de eventos de toohello que você acabou de criar:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Criar e excluir uma tabela Postgres
Agora que você conectou toohello banco de dados, você pode criar tabelas nele.

Por exemplo, crie uma nova tabela Postgres exemplo usando o comando a seguir de saudação:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Você já configurou uma tabela de quatro colunas com hello nomes de coluna e restrições a seguir:

1. Olá "nome" coluna tem foi limitada por Olá VARCHAR comando toobe em 20 caracteres.
2. coluna de "comida" Hello indica um item de comida Olá que fará com que cada pessoa. VARCHAR limita toobe esse texto em 30 caracteres.
3. Olá "confirmada" registros de coluna se a pessoa Olá tenha confirmado presença toohello americana. os valores aceitáveis Olá são "Y" e "N".
4. Data"Hello" coluna mostra quando eles se inscreveu para eventos de saudação. Postgres exige que as datas sejam gravadas como aaaa-mm-dd.

Você deve ver o seguinte Olá se sua tabela tiver sido criada com êxito:

![imagem](./media/postgresql-install/no4.png)

Você também pode verificar a estrutura da tabela hello usando Olá comando a seguir:

![imagem](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Adicionar dados tooa tabela
Primeiro, insira as informações em uma linha:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Você deverá ver este resultado:

![imagem](./media/postgresql-install/no6.png)

Você pode adicionar duas mais pessoas toohello tabela também. Aqui estão algumas opções, ou você pode criar as suas próprias:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Mostrar tabelas
Use Olá comando tooshow uma tabela a seguir:

    select * from potluck;

saída de Hello é:

![imagem](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Excluir dados de uma tabela
Saudação de usar dados de toodelete de comando em uma tabela a seguir:

    delete from potluck where name=’John’;

Isso exclui todas as informações de Olá Olá linha "John". saída de Hello é:

![imagem](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Atualizar dados em uma tabela
Use Olá seguintes comando tooupdate dados em uma tabela. Para esta, areia da confirmou que ela está participando, portanto, alteraremos sua RSVP de "N" muito "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Obter mais informações sobre o PostgreSQL
Agora que você concluiu a instalação de saudação do PostgreSQL em uma VM do Linux do Azure, você pode aproveitar a usá-lo no Azure. toolearn mais sobre PostgreSQL, visite Olá [PostgreSQL site](http://www.postgresql.org/).

