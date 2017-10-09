<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate um novo serviço

1. Use o toolog de credenciais de conta Microsoft em toohello [portal do Azure](https://portal.azure.com/).

2. No portal do Azure de Olá, clique em  **+**  e, em seguida, no marketplace hello, clique em **ver todos os**.

    ![Criar Gerenciador de Dispositivo StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Procure _StorSimple Físico_. Selecione e clique em **Série de Dispositivos Físicos StorSimple** e então clique em **Criar**. Como alternativa, no portal do Azure de saudação, clique em  **+**  e, em seguida, em **armazenamento**, clique em **série de dispositivo físico StorSimple**.

    ![Criar Gerenciador de Dispositivo StorSimple](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. Em Olá **Gerenciador de dispositivos de StorSimple** folha, Olá seguintes etapas:
   
   1. Forneça um **Nome do recurso** exclusivo para o serviço. Esse nome é um nome amigável que pode ser usado tooidentify Olá serviço. Olá nome pode ter entre 2 e 50 caracteres que podem ser letras, números e hifens. nome da saudação deve começar e terminar com uma letra ou um número.

   2. Escolha um **assinatura** da lista suspensa de saudação. assinatura de saudação é vinculado tooyour conta de cobrança. Este campo não estará presente se você tiver apenas uma assinatura.

   3. Para **Grupo de recursos**, **Usar existente** ou **Criar novo** grupo. Para obter mais informações, veja [Grupos de recursos do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Fornecer um **Local** para o serviço. Em geral, escolha um local mais próximo toohello região geográfica em que você deseja toodeploy seu dispositivo. Também convém toofactor em Olá considerações a seguir: 
      
      * Se você tiver cargas de trabalho existentes no Azure que você também pretende toodeploy com seu dispositivo StorSimple, você deve usar esse datacenter.
      * Seu serviço Gerenciador de Dispositivos StorSimple e o Armazenamento do Azure podem estar em dois locais separados. Nesse caso, será necessário toocreate Olá Gerenciador de dispositivos do StorSimple e conta de armazenamento do Azure separadamente. toocreate uma conta de armazenamento do Azure, vá toohello serviço de armazenamento do Azure no portal do Azure de saudação e siga etapas Olá [criar uma conta de armazenamento do Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Depois de criar essa conta, adicioná-lo toohello serviço de Gerenciador de dispositivos do StorSimple, seguindo as etapas de saudação em [configurar uma nova conta de armazenamento para o serviço de saudação](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Selecione **criar uma nova conta de armazenamento** tooautomatically criar uma conta de armazenamento com o serviço de saudação. Especifique um nome para essa conta de armazenamento. Se você precisar de seus dados em um local diferente, desmarque essa caixa.

   6. Verificar **toodashboard Pin** se você deseja um serviço de toothis de link rápido no seu painel.
      
   7. Clique em **criar** toocreate Olá Gerenciador de dispositivos do StorSimple.

       ![Criar Gerenciador de Dispositivo StorSimple](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
criação de serviço Olá leva alguns minutos. Depois que o serviço de saudação é criado com êxito, você verá uma notificação e nova folha de serviço Olá abre.
   
![Criar Gerenciador de Dispositivo StorSimple](./media/storsimple-8000-create-new-service/createssdevman5.png)


