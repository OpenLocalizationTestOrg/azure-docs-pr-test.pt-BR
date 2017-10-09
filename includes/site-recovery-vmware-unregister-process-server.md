<span data-ttu-id="27db5-101">Olá etapas toounregister um servidor de processo difere dependendo de seu status de conexão com servidor de configuração de hello.</span><span class="sxs-lookup"><span data-stu-id="27db5-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="27db5-102">Cancelar o registro de um servidor de processo que está em um estado conectado</span><span class="sxs-lookup"><span data-stu-id="27db5-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="27db5-103">Conexão remota para o servidor de processo hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="27db5-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="27db5-104">Iniciar Olá **painel de controle** e abra **programas > desinstalar um programa**</span><span class="sxs-lookup"><span data-stu-id="27db5-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="27db5-105">Desinstalar um programa pelo nome da saudação **servidor/processo de configuração de recuperação de Site do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="27db5-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="27db5-106">Após a conclusão da etapa 3, você pode desinstalar **dependências de servidor do Microsoft Azure Site Recovery/processo de configuração**</span><span class="sxs-lookup"><span data-stu-id="27db5-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="27db5-107">Cancelar o registro de um servidor de processo que está em um estado desconectado</span><span class="sxs-lookup"><span data-stu-id="27db5-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="27db5-108">Saudação de uso etapas a seguir deve ser usada se não houver nenhuma máquina virtual do modo toorevive Olá no qual saudação do servidor em processo foi instalado.</span><span class="sxs-lookup"><span data-stu-id="27db5-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="27db5-109">Faça logon no servidor de configuração de tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="27db5-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="27db5-110">Abra um prompt de comando administrativo e procure o diretório de toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="27db5-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="27db5-111">Agora execute o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="27db5-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="27db5-112">Isso apagará detalhes Olá saudação do servidor de processo do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="27db5-112">This will purge hello details of hello process server from hello system.</span></span>
