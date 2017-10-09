#### <a name="toocreate-a-new-service"></a>toocreate um novo serviço

1.  Usando suas credenciais de conta da Microsoft, faça logon toohello portal do Azure nesta URL: <https://portal.azure.com/>. Se implantar dispositivo Olá no portal do governo, faça logon em: <https://portal.azure.us/>

2.  No portal do Azure de Olá, clique em **+ novo** &gt; **armazenamento** &gt; **série Virtual StorSimple**.

    ![Criar novo serviço](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  Em Olá **Gerenciador de dispositivos de StorSimple** folha que é aberta, Olá a seguir:

    1.  Forneça um **Nome do recurso** exclusivo para o serviço. nome do recurso Olá é um nome amigável que pode ser usado tooidentify Olá serviço. Olá nome pode ter entre 2 e 50 caracteres que podem ser letras, números e hifens. nome da saudação deve começar e terminar com uma letra ou um número.

    2.  Escolha um **assinatura** da lista suspensa de saudação. assinatura de saudação é vinculado tooyour conta de cobrança. Este campo não estará presente se você tiver apenas uma assinatura.

    3.  Para **Grupo de recursos**, selecione um grupo de recursos existente ou crie um novo. Para obter mais informações, veja [Grupos de recursos do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).

    4.  Fornecer um **Local** para o serviço. Veja [Regiões do Azure](https://azure.microsoft.com/regions/#services) para saber mais sobre quais serviços estão disponíveis em qual região. Em geral, escolha um **local** região geográfica mais próxima do toohello onde você deseja toodeploy seu dispositivo. Também convém toofactor seguir hello:

        -   Se você tiver cargas de trabalho existentes no Azure que você também pretende toodeploy com seu dispositivo StorSimple, recomendamos que você use esse datacenter.

        -   O StorSimple Device Manager e o Armazenamento do Azure podem estar em duas localizações separadas. Nesse caso, será necessário toocreate Olá Gerenciador de dispositivos do StorSimple e conta de armazenamento do Azure separadamente. toocreate uma conta de armazenamento do Azure, vá toohello serviço de armazenamento do Azure no portal do Azure de saudação e siga etapas Olá [criar uma conta de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Depois de criar essa conta, adicioná-lo toohello serviço de Gerenciador de dispositivos do StorSimple, seguindo as etapas de saudação em [configurar uma nova conta de armazenamento para o serviço de saudação](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Se a implantação de dispositivo virtual Olá Olá Portal do governo, Olá serviço do Gerenciador de dispositivos de StorSimple está disponível em locais de Iowa conosco e nós Virgínia.

    5.  Selecione **criar uma nova conta de armazenamento do Azure** tooautomatically criar uma conta de armazenamento com o serviço de saudação. Especifique um **Nome de conta de armazenamento**. Se você precisar de seus dados em um local diferente, desmarque essa caixa.

    6.  Verificar **toodashboard Pin** se você deseja um serviço de toothis de link rápido no seu painel.

    7.  Clique em **criar** toocreate Olá Gerenciador de dispositivos do StorSimple.

        ![Criar novo serviço](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Você está direcionado toohello **Service** página inicial. criação de serviço Olá leva alguns minutos. Depois que o serviço Olá é criado com êxito, você será notificado adequadamente e status de saudação do serviço de saudação alterará muito**Active**.


