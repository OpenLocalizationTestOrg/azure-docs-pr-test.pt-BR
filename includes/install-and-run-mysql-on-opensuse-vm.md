
1. tooescalate privilégios, tipo:
   
        sudo -s
   
    Digite sua senha.
2. tooinstall Server do MySQL Community edition, digite:
   
        zypper install mysql-community-server
   
    Aguarde enquanto o MySQL é baixado e instalado.
3. tooset MySQL toostart quando Olá sistema é inicializado, digite:
   
        insserv mysql
4. Inicie o daemon do MySQL hello (mysqld) manualmente com este comando:
   
        rcmysql start
   
    status toocheck Olá Olá daemon do MySQL, digite:
   
        rcmysql status
   
    Olá toostop daemon do MySQL, digite:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Após a instalação, a senha de raiz de MySQL Olá é vazia por padrão. Recomendamos a execução de **mysql\_secure\_installation**, um script que ajuda a proteger o MySQL. script Hello solicita senha raiz do toochange Olá MySQL, remover contas de usuário anônimo, desabilite os logons remotos raiz, remover bancos de dados de teste e recarregar a tabela de privilégios de saudação. É recomendável que você responder Sim tooall dessas opções e altere a senha de raiz de saudação.
   > 
   > 
5. Digite este script de saudação toorun script de instalação do MySQL:
   
        mysql_secure_installation
6. Faça logon em tooMySQL:
   
        mysql -u root -p
   
    Digite a senha de raiz de MySQL hello (que você alterou na etapa anterior Olá) e você verá um prompt de onde você pode emitir toointeract de instruções SQL com o banco de dados de saudação.
7. toocreate um novo usuário do MySQL, execute o seguinte de saudação em Olá **mysql >** prompt:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Observe que, ponto e vírgula do hello (;) final Olá Olá linhas são cruciais para final de comandos de saudação.
8. toocreate um banco de dados e conceder Olá `mysqluser` usuário permissões, Olá problema comandos a seguir:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Observe que as senhas e nomes de usuário de banco de dados só são usadas por scripts conectar toohello banco de dados.  Nomes de conta de usuário de banco de dados não representa necessariamente a contas de usuário real no sistema de saudação.
9. toolog em de outro computador, digite:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    onde `ip-address` é o endereço IP de saudação do computador de saudação do qual você se conectará tooMySQL.
10. Olá tooexit utilitário de administração de banco de dados MySQL, digite:
    
        quit

## <a name="add-an-endpoint"></a>Adicionar um ponto de extremidade
1. Depois de instalar o MySQL, você precisará tooconfigure tooaccess um ponto de extremidade MySQL remotamente. Faça logon no toohello [portal clássico do Azure][AzurePortal]. Clique em **máquinas virtuais**, clique em nome de saudação da nova máquina virtual e, em seguida, clique em **pontos de extremidade**.
2. Clique em **adicionar** final Olá Olá página.
3. Adicionar um ponto de extremidade chamado "MySQL" com o protocolo **TCP**, e **pública** e **privada** portas conjunto muito "3306".
4. tooremotely conectar máquina virtual de toohello do seu computador, digite:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Por exemplo, usando a máquina virtual de saudação criado neste tutorial, digite este comando:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
