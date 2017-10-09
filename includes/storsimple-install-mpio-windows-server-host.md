#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO no host de saudação
1. Abra o Gerenciador de Servidores no host do Windows Server. Por padrão, o Gerenciador do servidor começa quando um membro do grupo de administradores Olá logon tooa computador que está executando o Windows Server 2012 R2 ou Windows Server 2012. Se o Gerenciador do servidor de saudação já não estiver aberta, clique em **Iniciar > Gerenciador de servidores**.
   
    ![Gerenciador de Servidores](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. Clique em **Gerenciador de Servidores > Painel de Controle > Adicionar funções e recursos**. Isso inicia o hello **adicionar funções e recursos** assistente.
   
    ![Adicionar Assistente de Funções e Recursos 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. Em Olá **adicionar funções e recursos** assistente, Olá a seguir:
   
   * Em Olá **antes de começar a** , clique em **próximo**.
   * Em Olá **Selecionar tipo de instalação** página, aceite a configuração padrão de saudação do **baseada em função ou recurso** instalação. Clique em **Avançar**.
     
       ![Adicionar Assistente de Funções e Recursos 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * Em Olá **Selecionar servidor de destino** escolha **selecionar um servidor do pool do servidor de saudação**. O servidor host deve ser descoberto automaticamente. Clique em **Avançar**.
   * Em Olá **selecionar funções de servidor** , clique em **próximo**.
   * Em Olá **selecionar recursos** , selecione **Multipath i / o**e clique em **próximo**.
     
       ![Adicionar Assistente de Funções e Recursos 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * Em Olá **confirmar seleções de instalação** página, confirmar seleção hello e, em seguida, selecione **reinicialização do servidor de destino Olá automaticamente, se necessário**, conforme mostrado abaixo. Clique em **Instalar**.
     
       ![Adicionar Assistente de Funções e Recursos 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * Você será notificado quando Olá instalação for concluída. Clique em **fechar** tooclose Assistente de saudação.
     
       ![Adicionar Assistente de Funções e Recursos 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

