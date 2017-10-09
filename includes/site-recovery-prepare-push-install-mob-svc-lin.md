### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Preparação para uma instalação por push em um servidor Linux

1. Certifique-se de que há conectividade de rede entre o computador Linux hello e servidor de processo hello.
2. Crie uma conta que nesse servidor de processo Olá usar tooaccess Olá computador. Olá conta deve ser um **raiz** usuário no servidor do hello origem Linux. (Usar essa conta somente para a instalação por push hello e para atualizações).
3. Verifique o arquivo /etc/hosts Olá na fonte Olá Linux server tem entradas que mapeiam Olá nome do host local tooIP endereços associados a todos os adaptadores de rede.
4. Instale pacotes de openssh, servidor openssh e openssl da mais recentes Olá no computador de saudação que você deseja tooreplicate.
5. Verifique se o Secure Shell (SSH) está habilitado e em execução na porta 22.
6. Habilite a autenticação de SFTP subsistema e a senha no arquivo de sshd_config hello:
  1.  Conecte-se como **raiz**.
  2.  Em Olá arquivo/etc/ssh/arquivo sshd_config, localizar Olá linha que começa com **PasswordAuthentication**.
  3.  Descomente a linha hello e altere o valor de saudação muito**Sim**.
  4.  Linha de saudação de localização que começa com **subsistema** e remova os comentários de linha de saudação.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Reiniciar Olá **sshd** serviço.

7. Adicione conta Olá que você criou na CSPSConfigtool.
    1.  Faça logon no servidor de configuração de tooyour.
    2.  Abra **cspsconfigtool.exe**. (Está disponível como um atalho na área de trabalho hello e na pasta de %ProgramData%\home\svsystems\bin hello.)
    3.  Em Olá **gerenciar contas** , clique em **adicionar conta**.
    4.  Adicione a conta de saudação criada. 
    5.  Insira credenciais Olá usadas quando você habilitar a replicação de um computador.
