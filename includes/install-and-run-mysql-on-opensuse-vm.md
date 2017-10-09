
1. <span data-ttu-id="e0f31-101">tooescalate privilégios, tipo:</span><span class="sxs-lookup"><span data-stu-id="e0f31-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="e0f31-102">Digite sua senha.</span><span class="sxs-lookup"><span data-stu-id="e0f31-102">Enter your password.</span></span>
2. <span data-ttu-id="e0f31-103">tooinstall Server do MySQL Community edition, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="e0f31-104">Aguarde enquanto o MySQL é baixado e instalado.</span><span class="sxs-lookup"><span data-stu-id="e0f31-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="e0f31-105">tooset MySQL toostart quando Olá sistema é inicializado, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="e0f31-106">Inicie o daemon do MySQL hello (mysqld) manualmente com este comando:</span><span class="sxs-lookup"><span data-stu-id="e0f31-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="e0f31-107">status toocheck Olá Olá daemon do MySQL, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="e0f31-108">Olá toostop daemon do MySQL, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="e0f31-109">Após a instalação, a senha de raiz de MySQL Olá é vazia por padrão.</span><span class="sxs-lookup"><span data-stu-id="e0f31-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="e0f31-110">Recomendamos a execução de **mysql\_secure\_installation**, um script que ajuda a proteger o MySQL.</span><span class="sxs-lookup"><span data-stu-id="e0f31-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="e0f31-111">script Hello solicita senha raiz do toochange Olá MySQL, remover contas de usuário anônimo, desabilite os logons remotos raiz, remover bancos de dados de teste e recarregar a tabela de privilégios de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f31-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="e0f31-112">É recomendável que você responder Sim tooall dessas opções e altere a senha de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f31-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="e0f31-113">Digite este script de saudação toorun script de instalação do MySQL:</span><span class="sxs-lookup"><span data-stu-id="e0f31-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="e0f31-114">Faça logon em tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="e0f31-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="e0f31-115">Digite a senha de raiz de MySQL hello (que você alterou na etapa anterior Olá) e você verá um prompt de onde você pode emitir toointeract de instruções SQL com o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f31-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="e0f31-116">toocreate um novo usuário do MySQL, execute o seguinte de saudação em Olá **mysql >** prompt:</span><span class="sxs-lookup"><span data-stu-id="e0f31-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e0f31-117">Observe que, ponto e vírgula do hello (;) final Olá Olá linhas são cruciais para final de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f31-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="e0f31-118">toocreate um banco de dados e conceder Olá `mysqluser` usuário permissões, Olá problema comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0f31-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e0f31-119">Observe que as senhas e nomes de usuário de banco de dados só são usadas por scripts conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e0f31-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="e0f31-120">Nomes de conta de usuário de banco de dados não representa necessariamente a contas de usuário real no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0f31-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="e0f31-121">toolog em de outro computador, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e0f31-122">onde `ip-address` é o endereço IP de saudação do computador de saudação do qual você se conectará tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="e0f31-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="e0f31-123">Olá tooexit utilitário de administração de banco de dados MySQL, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="e0f31-124">Adicionar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="e0f31-124">Add an endpoint</span></span>
1. <span data-ttu-id="e0f31-125">Depois de instalar o MySQL, você precisará tooconfigure tooaccess um ponto de extremidade MySQL remotamente.</span><span class="sxs-lookup"><span data-stu-id="e0f31-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="e0f31-126">Faça logon no toohello [portal clássico do Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="e0f31-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="e0f31-127">Clique em **máquinas virtuais**, clique em nome de saudação da nova máquina virtual e, em seguida, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="e0f31-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="e0f31-128">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="e0f31-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="e0f31-129">Adicionar um ponto de extremidade chamado "MySQL" com o protocolo **TCP**, e **pública** e **privada** portas conjunto muito "3306".</span><span class="sxs-lookup"><span data-stu-id="e0f31-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="e0f31-130">tooremotely conectar máquina virtual de toohello do seu computador, digite:</span><span class="sxs-lookup"><span data-stu-id="e0f31-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="e0f31-131">Por exemplo, usando a máquina virtual de saudação criado neste tutorial, digite este comando:</span><span class="sxs-lookup"><span data-stu-id="e0f31-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
