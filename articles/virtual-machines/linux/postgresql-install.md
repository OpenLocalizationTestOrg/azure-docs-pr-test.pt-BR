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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="84246-103">Instalar e configurar o PostgreSQL no Azure</span><span class="sxs-lookup"><span data-stu-id="84246-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="84246-104">PostgreSQL é tooOracle semelhante de banco de dados avançado do código-fonte aberto e DB2.</span><span class="sxs-lookup"><span data-stu-id="84246-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="84246-105">Ele inclui recursos corporativos como conformidade total com ACID, processamento transacional confiável e controle de simultaneidade de várias versões.</span><span class="sxs-lookup"><span data-stu-id="84246-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="84246-106">Também oferece suporte a padrões como ANSI SQL e SQL/MED (inclusive wrappers de dados externos para Oracle, MySQL, MongoDB e muitos outros).</span><span class="sxs-lookup"><span data-stu-id="84246-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="84246-107">Ele é altamente extensível com suporte para mais de 12 idiomas de procedimento, índices GIN e GiST, dados espaciais e vários recursos como NoSQL para aplicativos JSON ou de chave-valor.</span><span class="sxs-lookup"><span data-stu-id="84246-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="84246-108">Neste artigo, você aprenderá como tooinstall e configurar PostgreSQL em uma máquina virtual do Azure executando o Linux.</span><span class="sxs-lookup"><span data-stu-id="84246-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="84246-109">Instalar o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84246-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="84246-110">Você já deve ter uma máquina virtual do Azure executando o Linux em ordem toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="84246-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="84246-111">toocreate e configurar uma VM do Linux antes de continuar, consulte o [tutorial de VM do Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84246-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="84246-112">Nesse caso, use a porta 1999 como Olá PostgreSQL porta.</span><span class="sxs-lookup"><span data-stu-id="84246-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="84246-113">Conecte-se toohello VM do Linux criado por meio do PuTTY.</span><span class="sxs-lookup"><span data-stu-id="84246-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="84246-114">Se este for Olá pela primeira vez que você está usando uma VM do Linux do Azure, consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn como toouse PuTTY tooconnect tooa VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="84246-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="84246-115">Comando a seguir de execução Olá tooswitch toohello raiz (administrador):</span><span class="sxs-lookup"><span data-stu-id="84246-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="84246-116">Algumas distribuições têm dependências que devem ser instaladas antes de instalar o PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="84246-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="84246-117">Verifique a distribuição da lista e execute o comando apropriado hello:</span><span class="sxs-lookup"><span data-stu-id="84246-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="84246-118">Linux baseado em Red Hat:</span><span class="sxs-lookup"><span data-stu-id="84246-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="84246-119">Linux baseado em Debian:</span><span class="sxs-lookup"><span data-stu-id="84246-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="84246-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="84246-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="84246-121">Baixar PostgreSQL no diretório raiz de saudação e, em seguida, descompacte o pacote de saudação:</span><span class="sxs-lookup"><span data-stu-id="84246-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="84246-122">Olá acima é um exemplo.</span><span class="sxs-lookup"><span data-stu-id="84246-122">hello above is an example.</span></span> <span data-ttu-id="84246-123">Você pode encontrar hello mais detalhado baixar endereço no hello [índice de /pubfonte/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="84246-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="84246-124">compilação toostart hello, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="84246-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="84246-125">Se você quiser toobuild tudo o que pode ser criado, incluindo documentação hello (páginas HTML e man) e módulos adicionais (Contribuidor), execute Olá comando a seguir em vez disso:</span><span class="sxs-lookup"><span data-stu-id="84246-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="84246-126">Você deve receber Olá a seguinte mensagem de confirmação:</span><span class="sxs-lookup"><span data-stu-id="84246-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="84246-127">Configurar PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84246-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="84246-128">(Opcional) Criar uma saudação do link simbólico tooshorten PostgreSQL referência toonot incluem o número de versão de hello:</span><span class="sxs-lookup"><span data-stu-id="84246-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="84246-129">Crie um diretório para o banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="84246-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="84246-130">Crie um usuário não raiz e modifique o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="84246-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="84246-131">Em seguida, alternar toothis novo usuário (chamado *postgres* em nosso exemplo):</span><span class="sxs-lookup"><span data-stu-id="84246-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="84246-132">Por motivos de segurança, PostgreSQL usa tooinitialize um usuário não raiz, iniciar ou encerrar Olá banco de dados.</span><span class="sxs-lookup"><span data-stu-id="84246-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="84246-133">Editar saudação *bash_profile* arquivo digitando comandos de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="84246-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="84246-134">Essas linhas serão adicionadas toohello final de saudação *bash_profile* arquivo:</span><span class="sxs-lookup"><span data-stu-id="84246-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="84246-135">Executar Olá *bash_profile* arquivo:</span><span class="sxs-lookup"><span data-stu-id="84246-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="84246-136">Valide a instalação usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="84246-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="84246-137">Se a instalação for bem-sucedida, você verá Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="84246-138">Você também pode verificar a versão de PostgreSQL hello:</span><span class="sxs-lookup"><span data-stu-id="84246-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="84246-139">Inicialize o banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="84246-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="84246-140">Você deve receber Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-140">You should receive hello following output:</span></span>

![imagem](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="84246-142">Configurar o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84246-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="84246-143">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="84246-144">Modificar as duas variáveis no arquivo de /etc/init.d/postgresql hello.</span><span class="sxs-lookup"><span data-stu-id="84246-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="84246-145">Olá é definido toohello caminho de instalação do PostgreSQL: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="84246-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="84246-146">PGDATA é definir o caminho de armazenamento de dados toohello de PostgreSQL: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="84246-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![imagem](./media/postgresql-install/no2.png)

<span data-ttu-id="84246-148">Alterar Olá arquivo toomake-executável:</span><span class="sxs-lookup"><span data-stu-id="84246-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="84246-149">Inicie o PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="84246-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="84246-150">Verifique se o ponto de extremidade de saudação do PostgreSQL está em:</span><span class="sxs-lookup"><span data-stu-id="84246-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="84246-151">Você deve ver Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-151">You should see hello following output:</span></span>

![imagem](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="84246-153">Conecte-se o banco de dados do toohello Postgres</span><span class="sxs-lookup"><span data-stu-id="84246-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="84246-154">Alterne toohello postgres usuário novamente:</span><span class="sxs-lookup"><span data-stu-id="84246-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="84246-155">Crie um banco de dados Postgres:</span><span class="sxs-lookup"><span data-stu-id="84246-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="84246-156">Conecte-se o banco de dados de eventos de toohello que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="84246-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="84246-157">Criar e excluir uma tabela Postgres</span><span class="sxs-lookup"><span data-stu-id="84246-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="84246-158">Agora que você conectou toohello banco de dados, você pode criar tabelas nele.</span><span class="sxs-lookup"><span data-stu-id="84246-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="84246-159">Por exemplo, crie uma nova tabela Postgres exemplo usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="84246-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="84246-160">Você já configurou uma tabela de quatro colunas com hello nomes de coluna e restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="84246-161">Olá "nome" coluna tem foi limitada por Olá VARCHAR comando toobe em 20 caracteres.</span><span class="sxs-lookup"><span data-stu-id="84246-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="84246-162">coluna de "comida" Hello indica um item de comida Olá que fará com que cada pessoa.</span><span class="sxs-lookup"><span data-stu-id="84246-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="84246-163">VARCHAR limita toobe esse texto em 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="84246-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="84246-164">Olá "confirmada" registros de coluna se a pessoa Olá tenha confirmado presença toohello americana.</span><span class="sxs-lookup"><span data-stu-id="84246-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="84246-165">os valores aceitáveis Olá são "Y" e "N".</span><span class="sxs-lookup"><span data-stu-id="84246-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="84246-166">Data"Hello" coluna mostra quando eles se inscreveu para eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="84246-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="84246-167">Postgres exige que as datas sejam gravadas como aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="84246-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="84246-168">Você deve ver o seguinte Olá se sua tabela tiver sido criada com êxito:</span><span class="sxs-lookup"><span data-stu-id="84246-168">You should see hello following if your table has been successfully created:</span></span>

![imagem](./media/postgresql-install/no4.png)

<span data-ttu-id="84246-170">Você também pode verificar a estrutura da tabela hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-170">You can also check hello table structure by using hello following command:</span></span>

![imagem](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="84246-172">Adicionar dados tooa tabela</span><span class="sxs-lookup"><span data-stu-id="84246-172">Add data tooa table</span></span>
<span data-ttu-id="84246-173">Primeiro, insira as informações em uma linha:</span><span class="sxs-lookup"><span data-stu-id="84246-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="84246-174">Você deverá ver este resultado:</span><span class="sxs-lookup"><span data-stu-id="84246-174">You should see this output:</span></span>

![imagem](./media/postgresql-install/no6.png)

<span data-ttu-id="84246-176">Você pode adicionar duas mais pessoas toohello tabela também.</span><span class="sxs-lookup"><span data-stu-id="84246-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="84246-177">Aqui estão algumas opções, ou você pode criar as suas próprias:</span><span class="sxs-lookup"><span data-stu-id="84246-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="84246-178">Mostrar tabelas</span><span class="sxs-lookup"><span data-stu-id="84246-178">Show tables</span></span>
<span data-ttu-id="84246-179">Use Olá comando tooshow uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="84246-180">saída de Hello é:</span><span class="sxs-lookup"><span data-stu-id="84246-180">hello output is:</span></span>

![imagem](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="84246-182">Excluir dados de uma tabela</span><span class="sxs-lookup"><span data-stu-id="84246-182">Delete data in a table</span></span>
<span data-ttu-id="84246-183">Saudação de usar dados de toodelete de comando em uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="84246-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="84246-184">Isso exclui todas as informações de Olá Olá linha "John".</span><span class="sxs-lookup"><span data-stu-id="84246-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="84246-185">saída de Hello é:</span><span class="sxs-lookup"><span data-stu-id="84246-185">hello output is:</span></span>

![imagem](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="84246-187">Atualizar dados em uma tabela</span><span class="sxs-lookup"><span data-stu-id="84246-187">Update data in a table</span></span>
<span data-ttu-id="84246-188">Use Olá seguintes comando tooupdate dados em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="84246-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="84246-189">Para esta, areia da confirmou que ela está participando, portanto, alteraremos sua RSVP de "N" muito "Y":</span><span class="sxs-lookup"><span data-stu-id="84246-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="84246-190">Obter mais informações sobre o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84246-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="84246-191">Agora que você concluiu a instalação de saudação do PostgreSQL em uma VM do Linux do Azure, você pode aproveitar a usá-lo no Azure.</span><span class="sxs-lookup"><span data-stu-id="84246-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="84246-192">toolearn mais sobre PostgreSQL, visite Olá [PostgreSQL site](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="84246-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

