
1. <span data-ttu-id="140e3-101">Em Olá **conexões híbridas** folha, clique conexão híbrida de saudação você acabou de criar e clique em **configuração de ouvinte**.</span><span class="sxs-lookup"><span data-stu-id="140e3-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Clique em Configuração do Ouvinte](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="140e3-103">Olá **propriedades da conexão híbrida** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="140e3-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="140e3-104">Em **Gerenciador de Conexão híbrida local**, escolha **baixar e configurar manualmente**, salvar Olá baixado HybridConnectionManager.msi pacote e copiar a cadeia de caracteres de conexão de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="140e3-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Clique aqui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="140e3-106">Em um prompt de comando do administrador, digite Olá instalador de saudação do toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="140e3-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="140e3-107">Depois de saudação instalador é executado, clique em **agora não**, procure toohello %ProgramFiles%\Microsoft\HybridConnectionManager pasta, execute HCMConfigWizard.exe e clique em **Sim** em Olá **usuário Controle de conta de** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="140e3-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="140e3-108">Cole a cadeia de conexão do hello híbrida que você copiou anteriormente e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="140e3-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Instalando](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="140e3-110">Quando a saudação instalação for concluída, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="140e3-110">When hello install completes, click **Close**.</span></span>
   
    ![Clique em Fechar](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="140e3-112">Em Olá **conexões híbridas** folha, Olá **Status** coluna agora mostra **conectado**.</span><span class="sxs-lookup"><span data-stu-id="140e3-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Status Conectado](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

