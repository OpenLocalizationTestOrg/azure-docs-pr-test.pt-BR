Siga estas etapas tooinstall e execute o MongoDB em uma máquina virtual executando o Windows Server.

> [!IMPORTANT]
> Os recursos de segurança do MongoDB, como autenticação e associação com o endereço IP, não são habilitados por padrão. Recursos de segurança devem ser habilitados antes de implantar o ambiente de produção do MongoDB tooa.  Para obter mais informações, confira [Segurança e autenticação](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Depois de se conectar a máquina virtual de toohello usando a área de trabalho remota, abra o Internet Explorer da saudação **iniciar** menu na máquina virtual de saudação.
2. Selecione Olá **ferramentas** botão no canto superior direito da saudação.  Em **opções da Internet**, selecione Olá **segurança** guia e, em seguida, selecione Olá **Sites confiáveis** ícone e finalmente clique Olá **Sites** botão. Adicionar *https://\*. mongodb.org* toohello lista de sites confiáveis.
3. Vá muito[Downloads - MongoDB](https://www.mongodb.com/download-center#community).
4. Localize Olá **atual versão estável** de **Community Server**, selecione hello mais recente **64-bit** versão na coluna do Windows hello. Baixe e execute o instalador MSI de saudação.
5. Geralmente, o MongoDB é instalado em C:\Arquivos de Programas\MongoDB. Pesquisar variáveis de ambiente na área de trabalho hello e adicionar a variável de caminho de toohello Olá MongoDB binários path. Por exemplo, você pode encontrar binários Olá em C:\Program Files\MongoDB\Server\3.4\bin em seu computador.
6. Criar os diretórios de dados e log do MongoDB no disco de dados hello (como unidade **f:**) criado na Olá etapas anteriores. De **iniciar**, selecione **Prompt de comando** tooopen uma janela de prompt de comando.  Tipo:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun Olá banco de dados, execute:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Todas as mensagens de log são direcionado toohello *F:\MongoLogs\mongolog.log* de arquivos como mongod.exe server é iniciado e preallocates arquivos de diário. Pode levar vários minutos para o MongoDB toopreallocate arquivos de diário hello e comece a escutar conexões. prompt de comando Olá permanece voltada para essa tarefa enquanto a instância do MongoDB está em execução.
8. Olá toostart shell administrativo do MongoDB, abrir outra janela de comando do **iniciar** e Olá tipo comandos a seguir:

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

    banco de dados de saudação é criado pelo Olá insert.
9. Como alternativa, é possível instalar mongod.exe como um serviço:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    É instalado um serviço chamado MongoDB, com a descrição "Mongo DB". Olá `--logpath` opção deve ser usado toospecify um arquivo de log, pois Olá executar o serviço não tem uma saída toodisplay da janela de comando.  Olá `--logappend` opção especifica que uma reinicialização do serviço Olá faz com que o arquivo de log existente do saída tooappend toohello.  Olá `--dbpath` opção especifica o local de saudação do diretório de dados de saudação. Para obter mais opções de linha de comando relacionadas ao serviço, consulte [Opções de linha de comando relacionadas ao serviço][MongoWindowsSvcOptions].

    serviço de saudação toostart, execute este comando:

        C:\> net start MongoDB
10. Agora que o MongoDB está instalado e em execução, você precisa tooopen uma porta no Firewall do Windows assim você pode se conectar remotamente tooMongoDB.  De saudação **iniciar** menu, selecione **ferramentas administrativas** e **Firewall do Windows com segurança avançada**.
11. a) no painel esquerdo do hello, selecione **regras de entrada**.  Em Olá **ações** painel saudação à direita, selecione **nova regra...** .

    ![Firewall do Windows][Image1]

    b) na Olá **novo Assistente de regra de entrada**, selecione **porta** e, em seguida, clique em **próximo**.

    ![Firewall do Windows][Image2]

    Selecione **TCP** e **Portas locais específicas**.  Especifique uma porta de "27017" (porta de padrão Olá MongoDB escuta) e clique em **próximo**.

    ![Firewall do Windows][Image3]

    d) selecione **Permitir conexão Olá** e clique em **próximo**.

    ![Firewall do Windows][Image4]

    Clique em **Avançar** novamente.

    ![Firewall do Windows][Image5]

    f) Especifique um nome para a regra de saudação, como "MongoPort" e clique em **concluir**.

    ![Firewall do Windows][Image6]

12. Se você não configurar um ponto de extremidade para o MongoDB quando você criou a máquina virtual de saudação, você pode fazer isso agora. Você precisa de regra de firewall hello e Olá ponto de extremidade toobe capaz de tooconnect tooMongoDB remotamente.

  No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)**, clique em nome de saudação da nova máquina virtual e, em seguida, clique em **pontos de extremidade**.

    ![Pontos de extremidade][Image7]

13. Clique em **Adicionar**.

14. Adicionar um ponto de extremidade com o nome "Mongo", protocolo **TCP**e ambos **pública** e **privada** portas conjunto muito "27017". Esta porta permite toobe MongoDB acessado remotamente.

    ![Pontos de extremidade][Image9]

> [!NOTE]
> Olá porta 27017 é saudação padrão usado pelo MongoDB. Você pode alterar essa porta padrão especificando Olá `--port` parâmetro durante a inicialização do servidor de mongod.exe hello. Tornar toogive se Olá o mesmo número de porta no firewall hello e Olá ponto de extremidade de "Mongo" hello anterior instruções.
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
