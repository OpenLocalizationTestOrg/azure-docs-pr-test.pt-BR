<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar e formatar um volume
1. Inicie o iniciador iSCSI da Microsoft hello.
2. Em Olá **propriedades do iniciador iSCSI** janela Olá **descoberta** , clique em **descobrir Portal**.
3. Em Olá **descobrir Portal de destino** caixa de diálogo, forneça Olá endereço IP de sua interface de rede habilitada com iSCSI e, em seguida, clique em **Okey**. 
4. Em Olá **propriedades do iniciador iSCSI** janela Olá **destinos** guia, localize Olá **descobertos destinos**. status do dispositivo Olá devem aparecer como **inativo**.
5. Selecione o dispositivo de destino hello e, em seguida, clique em **conectar**. Depois Olá dispositivo estiver conectado, o status de saudação deve mudar muito**conectado**. (Para obter mais informações sobre como usar o iniciador iSCSI da Microsoft hello, consulte [instalando e configurando o Microsoft iSCSI Initiator][1]).
6. No host do Windows, pressione a tecla de logotipo do Windows hello + X e, em seguida, clique em **executar**. 
7. Em Olá **executar** caixa de diálogo, digite **Diskmgmt.msc**. Clique em **Okey**e hello **gerenciamento de disco** caixa de diálogo será exibida. painel direito da saudação mostrará volumes Olá em seu host.
8. Em Olá **gerenciamento de disco** janela, hello volumes montados serão exibidos conforme mostrado na ilustração a seguir de saudação. Com o botão direito volume Olá descoberto (clique em nome do disco Olá) e, em seguida, clique em **Online**.
   
     ![Inicializar formatação de volume](./media/storsimple-8000-mount-initialize-format-volume/step7initializeformatvolume.png) 
9. Clique com botão direito volume hello (clique em nome do disco Olá) novamente e, em seguida, clique em **inicializar**.
10. tooformat um volume simples, execute Olá etapas a seguir:
    
    1. Selecione o volume de saudação, clique duas vezes (clique na área da direita Olá) e clique em **Novo Volume simples**.
    2. No Assistente de novo Volume simples hello, especifique a letra de drive e tamanho do volume de hello e configurar o volume hello como um sistema de arquivos NTFS.
    3. Especifique um tamanho de unidade de alocação com 64 KB. Esse tamanho de unidade de alocação funciona bem com algoritmos de eliminação de duplicação de saudação usados em Olá solução StorSimple.
    4. Realize uma formatação rápida.

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
