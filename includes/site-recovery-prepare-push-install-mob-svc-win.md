### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Preparação para uma instalação por push em um computador Windows

1. Certifique-se de que há conectividade de rede entre o computador do Windows hello e servidor de processo hello.
2. Crie uma conta que nesse servidor de processo Olá usar tooaccess Olá computador. conta de saudação deve ter direitos de administrador (local ou domínio). (Usar essa conta somente para a instalação por push hello e para atualizações de agente).

   > [!NOTE]
   > Se você não estiver usando uma conta de domínio, desabilite o controle de acesso de usuário remoto no computador local hello. toodisable controle de acesso de usuário remoto, na chave de registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System hello, adicione um novo DWORD: **LocalAccountTokenFilterPolicy**. Defina o valor de saudação muito**1**. toodo isso em um comando prompt, execute Olá comando a seguir:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. No Firewall do Windows no computador de saudação desejado tooprotect, selecione **permitem que um aplicativo ou recurso pelo Firewall**. Habilite **Compartilhamento de Arquivo e Impressora** e **Instrumentação de Gerenciamento do Windows (WMI)**. Para computadores que pertencem a tooa domínio, você pode configurar as configurações do firewall hello usando um objeto de diretiva de grupo (GPO).

   ![Configurações de firewall](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Adicione conta Olá que você criou na CSPSConfigtool.
    1.  Faça logon no servidor de configuração de tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponível como um atalho na área de trabalho hello e na pasta de %ProgramData%\home\svsystems\bin hello.)
    3.  Em Olá **gerenciar contas** guia, selecione **adicionar conta**.
    4.  Adicione a conta de saudação criada.
    5.  Insira credenciais Olá usadas quando você habilitar a replicação de um computador.
