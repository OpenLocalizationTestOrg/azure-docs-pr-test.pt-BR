Olá etapas toounregister um servidor de processo difere dependendo de seu status de conexão com servidor de configuração de hello.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Cancelar o registro de um servidor de processo que está em um estado conectado

1. Conexão remota para o servidor de processo hello como administrador.
2. Iniciar Olá **painel de controle** e abra **programas > desinstalar um programa**
3. Desinstalar um programa pelo nome da saudação **servidor/processo de configuração de recuperação de Site do Microsoft Azure**
4. Após a conclusão da etapa 3, você pode desinstalar **dependências de servidor do Microsoft Azure Site Recovery/processo de configuração**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Cancelar o registro de um servidor de processo que está em um estado desconectado

> [!WARNING]
> Saudação de uso etapas a seguir deve ser usada se não houver nenhuma máquina virtual do modo toorevive Olá no qual saudação do servidor em processo foi instalado.

1. Faça logon no servidor de configuração de tooyour como um administrador.
2. Abra um prompt de comando administrativo e procure o diretório de toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Agora execute o comando de saudação.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Isso apagará detalhes Olá saudação do servidor de processo do sistema de saudação.
