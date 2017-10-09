1. Clicar em **Conectar** cria e baixa um arquivo .rdp (Protocolo de Área de Trabalho Remota). Clique em **abrir** toouse esse arquivo.
2. Você receberá um aviso que. rdp de saudação for de um editor desconhecido. Isso é normal. Na janela de área de trabalho remota hello, clique em **conectar** toocontinue.
   
    ![Captura de tela de um aviso sobre um editor desconhecido.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. Em Olá **a segurança do Windows** janela, digite as credenciais de saudação para uma conta na máquina virtual de saudação e, em seguida, clique em **Okey**.
   
     **Conta local** -isso é geralmente conta local de Olá Olá nome de usuário e senha que você especificou quando criou a máquina virtual. Nesse caso, domínio Olá é o nome de saudação da máquina virtual de saudação e ele é inserido como *vmname*&#92; *nome de usuário*.  
   
    **VM ingressado no domínio** - se Olá VM pertence tooa domínio, insira o nome de usuário de saudação em formato de saudação *domínio*&#92; *Nome de usuário*. conta de saudação também precisa tooeither ser Olá administradores de grupo ou ter privilégios de acesso remoto toohello VM.
   
    **Controlador de domínio** - se Olá VM for um controlador de domínio, o nome de usuário do tipo hello e a senha de uma conta de administrador de domínio para esse domínio.
4. Clique em **Sim** tooverify Olá identidade da máquina virtual de saudação e concluir o registro em log.
   
   ![Captura de tela mostrando uma mensagem limitam a verificar a identidade de saudação do hello VM.](./media/virtual-machines-log-on-win-server/cert-warning.png)

