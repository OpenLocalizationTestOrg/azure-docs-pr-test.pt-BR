## <a name="download-install-and-register-hello-azure-backup-agent"></a>Baixar, instalar e registrar o agente de Backup do Azure Olá
Depois de criar o Cofre de Backup do Azure hello, um agente deve ser instalado em cada uma de suas máquinas do Windows (Windows Server, Windows client, servidor do System Center Data Protection Manager ou máquina do servidor de Backup do Azure) que permite fazer backup de dados e aplicativos tooAzure.

1. Entrar toohello [Portal de gerenciamento](https://manage.windowsazure.com/)
2. Clique em **dos serviços de recuperação**, em seguida, selecione o Cofre de backup Olá que você deseja tooregister com um servidor. página de início rápido de saudação para esse Cofre de backup é exibida.
   
    ![Início rápido](./media/backup-install-agent/quickstart.png)
3. Na página de início rápido de saudação, clique em Olá **cliente para o Windows Server ou System Center Data Protection Manager ou Windows** opção em **baixar o agente**. Clique em **salvar** toocopy-computador local toohello.
   
    ![Salvar agente](./media/backup-install-agent/agent.png)
4. Depois de instalar o agente hello, clique duas vezes em instalação de saudação toolaunch MARSAgentInstaller.exe do agente de Backup do Azure hello. Escolha pasta de instalação hello e necessárias para o agente de saudação de pasta de rascunho. local do cache Olá especificado deve ter espaço livre, que é pelo menos 5% dos dados de backup de saudação.
5. Se você usar um toohello de tooconnect de servidor proxy internet, Olá **configuração de Proxy** tela, insira os detalhes do servidor proxy hello. Se você usar um proxy autenticado, insira os detalhes de nome e a senha do usuário Olá nesta tela.
6. Agente de Backup do Azure Olá realizou .NET Framework 4.5 e o Windows PowerShell (se já não estiver disponível) toocomplete Olá instalação.
7. Depois de instalar o agente hello, clique em Olá **continuar tooRegistration** toocontinue botão ao fluxo de trabalho de saudação.
   
   ![Registrar](./media/backup-install-agent/register.png)
8. Na tela de credenciais do cofre hello, procure tooand Olá selecione cofre arquivo de credenciais que foi baixado anteriormente.
   
    ![Credenciais do cofre](./media/backup-install-agent/vc.png)
   
    o arquivo de credenciais de cofre Olá é válido somente para 48 horas (depois que ele é baixado do portal de saudação). Se você encontrar qualquer erro nesta tela (por exemplo "credenciais do cofre arquivo fornecido expirou"), logon toohello portal do Azure e baixar credenciais do cofre Olá arquivo novamente.
   
    Certifique-se de que esse arquivo de credenciais de cofre hello está disponível em um local que pode ser acessado pelo aplicativo de instalação hello. Se você encontrar erros relacionados de acesso, credenciais do cofre Olá cópia arquivo local temporário de tooa nesta máquina e repita a operação de saudação.
   
    Se você encontrar um erro de credencial de Cofre inválido (por exemplo "inválido credenciais do cofre fornecidas") o arquivo hello está corrompido ou não têm Olá últimas credenciais associadas ao serviço de recuperação de saudação. Repita a operação Olá após o download de um novo arquivo de credencial do cofre no portal de saudação. Esse erro é geralmente visto se usuário Olá clicar em Olá **credencial do cofre Download** opção no portal do Azure, em sucessão rápida de saudação. Nesse caso, somente Olá segundo cofre credencial arquivo é válido.
9. Em Olá **configuração de criptografia** tela, você pode gerar uma senha ou forneça uma senha (mínimo de 16 caracteres). Lembre-se toosave Olá senha em um local seguro.
   
    ![Criptografia](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Se hello senha for perdida ou esquecida; Microsoft não pode ajudar na recuperação de dados de backup hello. usuário final de saudação possui Olá senha de criptografia e a Microsoft não tem visibilidade Olá senha usada pelo usuário final de saudação. Salve o arquivo de saudação em um local seguro conforme necessário durante uma operação de recuperação.
   > 
   > 
10. Depois de clicar em Olá **concluir** botão, hello máquina é registrada com êxito toohello cofre e você agora está pronto toostart backup tooMicrosoft do Azure.
11. Ao usar o Backup do Microsoft Azure autônomo você pode modificar configurações de saudação especificadas durante o fluxo de trabalho do hello registro clicando no hello **alterar propriedades** hello Azure Backup mmc snap-in de opção.
    
    ![Alterar propriedades](./media/backup-install-agent/change.png)
    
    Como alternativa, ao usar o Data Protection Manager, você pode modificar configurações de saudação especificadas durante o fluxo de trabalho do hello registro clicando Olá **configurar** opção selecionando **Online** em Olá **Gerenciamento** guia.
    
    ![Configurar o Backup do Azure](./media/backup-install-agent/configure.png)

