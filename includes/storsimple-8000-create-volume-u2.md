<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate um volume
1. Da lista tabular de saudação de dispositivos Olá Olá **dispositivos** folha, selecione seu dispositivo. Clique em **+ Adicionar volume**.

    ![Adicionar um novo volume](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. Em Olá **adicionar um volume** folha:
   
   1. Olá **Selecione dispositivo** campo será preenchido automaticamente com o dispositivo atual.

   2. Da lista suspensa de saudação, selecione o contêiner de volume de saudação em que você precisa tooadd um volume. 

   3.  Digite uma **Nome** para o seu volume. Após criar o volume de saudação não é possível renomear um volume.

   4. Na lista suspensa de hello, selecione Olá **tipo** para seu volume. Para cargas de trabalho que exigem garantias locais, menos latências e um melhor desempenho, selecione um volume **Fixado localmente** . Para todos os outros dados, selecione um volume **Em camadas** . Se estiver usando esse volume para dados de arquivamento, marque **Usar este volume para dados de arquivamento acessados com menos frequência**.
      
       Um volume em camadas é provisionado por completo e pode ser criado rapidamente. Selecionando **usar este volume para dados de arquivamento acessados com frequência menos** de volume em camadas direcionado para o tamanho de bloco de eliminação de duplicação dados de arquivamento alterações Olá para seu volume too512 KB. Se esse campo não estiver marcado, o volume de em camadas correspondente Olá usa um tamanho de bloco de 64 KB. Um tamanho de bloco de eliminação de duplicação maior permite a transferência de saudação do hello dispositivo tooexpedite da nuvem de toohello grandes de dados de arquivamento.
       
       Um volume localmente afixado é muito provisionado e garante que os dados primários de saudação no volume de saudação permanece dispositivo toohello local e não despejar toohello nuvem.  Se você criar um volume localmente afixado, Olá dispositivo verificará o espaço disponível nas camadas local Olá tooprovision volume de saudação do hello solicitado tamanho. operação Olá de criação de um volume localmente afixado pode envolver o despejo de dados existentes da nuvem de toohello dispositivo hello e tempo Olá volume de saudação toocreate pode ser longo. tempo total de saudação depende do tamanho de saudação do volume Olá provisionado, largura de banda disponível e dados Olá em seu dispositivo.

   5. Especifique a saudação **capacidade provisionada** para seu volume. Tome nota da capacidade de saudação que está disponível com base no tipo de volume de saudação selecionado. Olá especificado o tamanho do volume não deve exceder o espaço disponível de saudação.
      
       Você pode provisionar volumes em camadas até too200 TB no dispositivo 8100 Olá ou volumes localmente afixados backup too8.5 TB. No dispositivo 8600 maior de saudação, você pode provisionar volumes localmente afixados backup too22.5 TB ou volumes em camadas até too500 TB. Como espaço local no dispositivo Olá Olá toohost necessário trabalho conjunto de volumes em camadas, criação de volumes localmente afixados afeta Olá espaço disponível para provisionar volumes em camadas. Portanto, se você criar um volume fixado localmente, o espaço disponível para a criação de volumes em camadas será reduzido. Da mesma forma, se for criado um volume em camadas, espaço disponível de saudação para a criação de volumes localmente afixados é reduzido.
      
       Se você provisionar um volume localmente afixado de 8,5 TB (tamanho máximo permitido) em seu dispositivo 8100, você ter esgotado todo Olá local o espaço disponível no dispositivo de saudação. Você não pode criar qualquer volume em camadas desse ponto em diante, pois não há nenhum espaço local no conjunto de trabalho de Olá Olá dispositivo toohost de saudação hierárquico de volume. Volumes em camadas existentes também afetam o espaço de saudação disponível. Por exemplo, se você tiver um dispositivo 8100 que já tem volumes em camadas de 106 TB, somente 4 TB de espaço estarão disponíveis para volumes fixados localmente.

    6. Em Olá **conectado hosts** , clique em seta hello. 

        ![Hosts conectados](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. Em Olá **conectado hosts** folha, escolha um ACR existente ou adicionar um novo ACR executando Olá etapas a seguir:

       1. Dê um **Nome** para o seu ACR.
       2. Em **nome do iniciador iSCSI**, fornecer Olá iSCSI IQN (nome qualificado) do seu host do Windows. Se você não tiver Olá IQN, vá muito[Get hello IQN de um host do Windows Server](#get-the-iqn-of-a-windows-server-host).

    9. Clique em **Criar**. Um volume é criado com hello especificado as configurações.

        ![Clicar em Criar](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Lembre-se de que o volume de saudação criadas aqui não está protegido. Você precisará toocreate e associadas políticas de backup com backups de tootake agendado este volume. 

