<!--author=alkohli last changed:01/14/2016-->


#### <a name="toocreate-a-new-service"></a>toocreate um novo serviço
1. Usando suas credenciais de conta da Microsoft, faça logon toohello portal clássico do Azure nesta URL: [https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. No portal clássico do Azure do hello, clique em **novo** > **Data Services** > **StorSimple Manager** > **rápido Criar**.
3. No formulário de saudação que é exibido, Olá a seguir:
   
   1. Fornecer um **Nome** exclusivo para o serviço. Este é um nome amigável que pode ser usado tooidentify Olá serviço. Olá nome pode ter entre 2 e 50 caracteres que podem ser letras, números e hifens. nome da saudação deve começar e terminar com uma letra ou um número.
   2. Fornecer um **Local** para o serviço. Em geral, escolha um local mais próximo toohello região geográfica em que você deseja toodeploy seu dispositivo. Também convém toofactor seguir hello: 
      
      * Se você tiver cargas de trabalho existentes no Azure que você também pretende toodeploy com seu dispositivo StorSimple, você deve usar esse datacenter.
      * Seu serviço StorSimple Manager e o Armazenamento do Azure podem estar em dois locais separados. Nesse caso, será necessário toocreate Olá StorSimple Manager e a conta de armazenamento do Azure separadamente. toocreate uma conta de armazenamento do Azure, vá toohello serviço de armazenamento do Azure no portal clássico do Azure de saudação e siga etapas Olá [criar uma conta de armazenamento do Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Depois de criar essa conta, adicioná-lo o serviço StorSimple Manager toohello, seguindo as etapas de saudação em [configurar uma nova conta de armazenamento para o serviço de saudação](../articles/storsimple/storsimple-deployment-walkthrough.md#configure-a-new-storage-account-for-the-service).
   3. Escolha um **assinatura** da lista suspensa de saudação. assinatura de saudação é vinculado tooyour conta de cobrança. Este campo não estará presente se você tiver apenas uma assinatura.
   4. Selecione **criar uma nova conta de armazenamento** tooautomatically criar uma conta de armazenamento com o serviço de saudação. Esta conta de armazenamento terá um nome especial, como "storsimplebwv8c6dcnf". Se você precisar de seus dados em um local diferente, desmarque essa caixa. 
   5. Clique em **criar Gerenciador do StorSimple** toocreate serviço de saudação.
   
   ![Criar StorSimple Manager](./media/storsimple-create-new-service/HCS_CreateAService-include.png)
   
   Você será direcionado toohello **Service** página inicial. criação de serviço de saudação levará alguns minutos. Depois que o serviço Olá é criado com êxito, você será notificado adequadamente e status de saudação do serviço de saudação alterará muito**Active**.
   
   ![Criação de serviço](./media/storsimple-create-new-service/HCS_StorSimpleManagerServicePage-include.png)

![Vídeo disponível](./media/storsimple-create-new-service/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocreate um novo serviço StorSimple Manager, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-manager-service/).

