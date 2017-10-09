<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate um volume
1. No dispositivo Olá **início rápido** , clique em **adicionar um volume**. Isso inicia o Assistente adicionar um volume de saudação.
2. Em hello Assistente de adição de um volume, em **configurações básicas**, Olá a seguir:
   
   1. Digite um **Nome** para o seu volume.
   2. Especifique a saudação **capacidade provisionada** para seu volume em GB ou TB. a capacidade de volume Olá deve estar entre 1 GB e 64 TB para um dispositivo físico.
   3. Na lista suspensa de hello, selecione Olá **tipo de uso** para seu volume. 
   4. Se você estiver usando este volume para dados de arquivamento, selecione Olá **usar este volume para dados de arquivamento acessados com frequência menos** caixa de seleção. Para todos os outros casos de uso, selecione **Volume em Camadas**. (Volumes em camadas eram chamados anteriormente de volumes primários).
      
        ![Adicionar volume](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Clique no ícone de seta Olá ![ícone-de-seta](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello próxima página.
3. Em Olá **configurações adicionais** caixa de diálogo, adicione um novo registro de controle de acesso (ACR):
   
   1. Dê um **Nome** para o seu ACR.
   2. Em **nome do iniciador iSCSI**, fornecer Olá iSCSI IQN (nome qualificado) do seu host do Windows. Se você não tiver Olá IQN, vá muito[Get hello IQN de um host do Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Recomendamos que você habilite um backup padrão selecionando Olá **habilitar um backup padrão para este volume** caixa de seleção. backup de padrão de saudação criará uma política que é executado às 22:30 por dia (hora do dispositivo) e cria um instantâneo de nuvem deste volume.
      
      > [!NOTE]
      > Depois que o backup de saudação é ativado aqui, ele não pode ser revertido. Você precisará tooedit Olá volume toomodify essa configuração.
      > 
      > 
      
        ![Adicionar volume](./media/storsimple-create-volume/AddVolume2-include.png)
4. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Um volume será criado com hello especificado as configurações.

![Vídeo disponível](./media/storsimple-create-volume/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocreate um volume StorSimple, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

