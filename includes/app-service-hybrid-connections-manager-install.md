
1. Em Olá **conexões híbridas** folha, clique conexão híbrida de saudação você acabou de criar e clique em **configuração de ouvinte**.
   
    ![Clique em Configuração do Ouvinte](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Olá **propriedades da conexão híbrida** folha é aberta. Em **Gerenciador de Conexão híbrida local**, escolha **baixar e configurar manualmente**, salvar Olá baixado HybridConnectionManager.msi pacote e copiar a cadeia de caracteres de conexão de gateway hello.
   
    ![Clique aqui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Em um prompt de comando do administrador, digite Olá instalador de saudação do toostart de comando a seguir:
   
        start HybridConnectionManager.msi
4. Depois de saudação instalador é executado, clique em **agora não**, procure toohello %ProgramFiles%\Microsoft\HybridConnectionManager pasta, execute HCMConfigWizard.exe e clique em **Sim** em Olá **usuário Controle de conta de** caixa de diálogo.
5. Cole a cadeia de conexão do hello híbrida que você copiou anteriormente e clique em **Okey**. 
   
    ![Instalando](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Quando a saudação instalação for concluída, clique em **fechar**.
   
    ![Clique em Fechar](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    Em Olá **conexões híbridas** folha, Olá **Status** coluna agora mostra **conectado**. 
   
    ![Status Conectado](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

