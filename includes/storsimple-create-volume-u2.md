<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate um volume
1. No dispositivo Olá **início rápido** , clique em **adicionar um volume** toostart Olá Assistente adicionar um volume.
2. Em hello Assistente de adição de um volume, em **configurações básicas**:
   
   1. Digite uma **Nome** para o seu volume.
   2. Na lista suspensa de hello, selecione Olá **tipo de uso** para seu volume. Para cargas de trabalho que exigem garantias locais, menos latências e um melhor desempenho, selecione um volume **Fixado localmente** . Para todos os outros dados, selecione um volume **Em camadas** . Se estiver usando esse volume para dados de arquivamento, marque **Usar este volume para dados de arquivamento acessados com menos frequência**. 
      
       Um volume localmente afixado é muito provisionado e garante que os dados primários de saudação no volume de saudação permanece dispositivo toohello local e não despejar toohello nuvem.  Se você criar um volume localmente afixado, Olá dispositivo verificará o espaço disponível nas camadas local Olá tooprovision volume de saudação do hello solicitado tamanho. operação Olá de criação de um volume localmente afixado pode envolver o despejo de dados existentes da nuvem de toohello dispositivo hello e tempo Olá volume de saudação toocreate pode ser longo. tempo total de saudação depende do tamanho de saudação do volume Olá provisionado, largura de banda disponível e dados Olá em seu dispositivo. 
      
       Um volume em camadas é provisionado por completo e pode ser criado rapidamente. Selecionando **usar este volume para dados de arquivamento acessados com frequência menos** de volume em camadas direcionado para o tamanho de bloco de eliminação de duplicação dados de arquivamento alterações Olá para seu volume too512 KB. Se esse campo não estiver marcado, o volume de em camadas correspondente Olá usa um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento.
   3. Especifique a saudação **capacidade provisionada** para seu volume. Tome nota da capacidade de saudação que está disponível com base no tipo de volume de saudação selecionado. Olá especificado o tamanho do volume não deve exceder o espaço disponível de saudação.
      
       Você pode provisionar volumes em camadas até too200 TB no dispositivo 8100 Olá ou volumes localmente afixados backup too8.5 TB. No dispositivo 8600 maior de saudação, você pode provisionar volumes localmente afixados backup too22.5 TB ou volumes em camadas até too500 TB. Como espaço local no dispositivo Olá Olá toohost necessário trabalho conjunto de volumes em camadas, criação de volumes localmente afixados afeta Olá espaço disponível para provisionar volumes em camadas. Portanto, se você criar um volume fixado localmente, o espaço disponível para a criação de volumes em camadas será reduzido. Da mesma forma, se for criado um volume em camadas, espaço disponível de saudação para a criação de volumes localmente afixados é reduzido.
      
       Se você provisionar um volume localmente afixado de 8,5 TB (tamanho máximo permitido) em seu dispositivo 8100, você ter esgotado todo Olá local o espaço disponível no dispositivo de saudação. Você não será capaz de toocreate qualquer volume em camadas do ponto em diante, como há está sem espaço local no conjunto de trabalho de Olá Olá dispositivo toohost de saudação em camadas no volume. Volumes em camadas existentes também afetam o espaço de saudação disponível. Por exemplo, se você tiver um dispositivo 8100 que já tem volumes em camadas de 106 TB, somente 4 TB de espaço estarão disponíveis para volumes fixados localmente.
      
       Olá, imagem a seguir mostra Olá **configurações básicas** caixa de diálogo para um volume localmente afixado.
      
        ![Adicionar volume local](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Olá, imagem a seguir mostra Olá **configurações básicas** caixa de diálogo para um volume em camadas.
      
        ![Adicionar volume local](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Clique no ícone de seta Olá ![ícone-de-seta](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello próxima página.
3. Em Olá **configurações adicionais** caixa de diálogo, adicione um novo registro de controle de acesso (ACR):
   
   1. Dê um **Nome** para o seu ACR.
   2. Em **nome do iniciador iSCSI**, fornecer Olá iSCSI IQN (nome qualificado) do seu host do Windows. Se você não tiver Olá IQN, vá muito[Get hello IQN de um host do Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Em **backup padrão para este volume?**, selecione Olá **habilitar** caixa de seleção. backup de padrão de saudação cria uma política que é executado às 22:30 por dia (hora do dispositivo) e cria um instantâneo de nuvem deste volume.
      
      > [!NOTE]
      > Depois que o backup de saudação é ativado aqui, ele não pode ser revertido. É necessário tooedit Olá volume toomodify essa configuração.
      > 
      > 
      
      ![Adicionar volume](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Um volume é criado com hello especificado as configurações.

