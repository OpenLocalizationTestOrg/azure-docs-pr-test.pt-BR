Siga estas etapas para instalar e executar o MongoDB em uma máquina virtual que executa o Windows Server.

> [!IMPORTANT]
> Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão. Os recursos de segurança devem ser ativados antes de implantar o MongoDB em um ambiente de produção.  Para obter mais informações, confira [Segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Depois de se conectar à máquina virtual usando a Área de Trabalho Remota, abra o Internet Explorer usando o menu **Iniciar** da máquina virtual.
2. Selecione o botão **Ferramentas** no canto superior direito.  Em **Opções da Internet**, selecione a guia **Segurança**, selecione o ícone **Sites confiáveis** e, por fim, clique no botão **Sites**. Adicione *https://\*.mongodb.org* à lista de sites confiáveis.
3. Acesse [Downloads- MongoDB](https://www.mongodb.com/download-center#community).
4. Encontre a **Compilação Estável Atual** de **Community Server** e selecione a mais recente versão de **64 bits** na coluna Windows. Baixe e execute o instalador MSI.
5. Geralmente, o MongoDB é instalado em C:\Arquivos de Programas\MongoDB. Procure pelas Variáveis de Ambiente na área de trabalho e adicione o caminho dos binários do MongoDB à variável PATH. Por exemplo, você pode localizar os binários em C:\Arquivos de Programas\MongoDB\Server\3.4\bin em seu computador.
6. Crie diretórios de dados e de log do MongoDB no disco de dados (como a unidade **F:**) criado nas etapas anteriores. No menu **Iniciar**, selecione **Prompt de Comando** para abrir uma janela do prompt de comando.  Tipo:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. Para executar o banco de dados, execute:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Todas as mensagens de log serão direcionadas ao arquivo *F:\MongoLogs\mongolog.log* quando o servidor mongod.exe for iniciado e pré-alocar arquivos de diário. Pode levar alguns minutos para que o MongoDB pré-aloque os arquivos de diário e comece a detectar conexões. O prompt de comando permanece focado nessa tarefa enquanto sua instância do MongoDB está em execução.
8. Para iniciar o shell administrativo do MongoDB, abra outra janela Comando no menu **Iniciar** e digite:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    O banco de dados é criado pelo comando insert.
9. Como alternativa, é possível instalar mongod.exe como um serviço:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    É instalado um serviço chamado MongoDB, com a descrição "Mongo DB". A opção `--logpath` deve ser usada para especificar um arquivo de log uma vez que o serviço em execução não terá uma janela de comando para exibir a saída.  A opção `--logappend` especifica que uma reinicialização do serviço fará com que a saída seja acrescentada ao arquivo de log existente.  A opção `--dbpath` especifica o local do diretório de dados. Para obter mais opções de linha de comando relacionadas ao serviço, consulte [Opções de linha de comando relacionadas ao serviço][MongoWindowsSvcOptions].

    Para iniciar o serviço, execute este comando:

        C:\> net start MongoDB
10. Agora que o MongoDB está instalado e em execução, você precisa abrir uma porta no Firewall do Windows para poder se conectar remotamente ao MongoDB.  No menu **Iniciar**, selecione **Ferramentas Administrativas** e depois **Firewall do Windows com segurança avançada**.
11. No painel esquerdo, selecione **Regras de Entrada**.  À direita, no painel **Ações**, selecione **Nova Regra...**.

    ![Firewall do Windows][Image1]

    No **Assistente para Nova Regra de Entrada**, selecione **Porta** e clique em **Avançar**.

    ![Firewall do Windows][Image2]

    Selecione **TCP** e **Portas locais específicas**.  Especifique uma porta "27017" (a porta padrão em que MongoDB escuta) e clique em **Avançar**.

    ![Firewall do Windows][Image3]

    Selecione **Permitir a conexão** e clique em **Avançar**.

    ![Firewall do Windows][Image4]

    Clique em **Avançar** novamente.

    ![Firewall do Windows][Image5]

    Especifique um nome para a regra, como "MongoPort", e clique em **Concluir**.

    ![Firewall do Windows][Image6]

12. Se você não configurou um ponto de extremidade para o MongoDB quando criou a máquina virtual, pode fazer isso agora. Você precisa do ponto de extremidade e da regra de firewall para ser capaz de se conectar remotamente ao MongoDB.

  No portal do Azure, clique em **Máquinas Virtuais (clássicas)**, clique no nome de sua nova máquina virtual e clique em **Pontos de Extremidade**.

    ![Pontos de extremidade][Image7]

13. Clique em **Adicionar**.

14. Adicione um ponto de extremidade com o nome "Mongo", protocolo **TCP** e defina as portas **Pública** e **Privada** como "27017". Abrir essa porta permite que o MongoDB seja acessado remotamente.

    ![Pontos de extremidade][Image9]

> [!NOTE]
> A porta 27017 é a porta padrão usada pelo MongoDB. Você pode alterar essa porta padrão especificando o parâmetro `--port` ao iniciar o servidor mongod.exe. Forneça o mesmo número de porta no firewall e no ponto de extremidade "Mongo" nas instruções anteriores.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
