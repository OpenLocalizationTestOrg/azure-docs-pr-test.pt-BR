## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Usando tooauthenticate de credenciais de cofre com hello serviço Backup do Azure
servidor de local de saudação (Windows cliente ou servidor Windows Server ou do Data Protection Manager) precisa toobe autenticado com um cofre de backup antes que ele pode fazer backup de dados tooAzure. autenticação de saudação é obtida usando o "cofre credenciais". conceito de saudação de credenciais do cofre é conceito toohello semelhante de um arquivo de "configurações de publicação" que é usado no Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>O que é o arquivo de credencial de cofre Olá?
o arquivo de credenciais de cofre Olá é um certificado gerado pelo portal Olá para cada Cofre de backup. portal de saudação carrega toohello chave pública Olá Access Control Service (ACS). chave privada de saudação do certificado de saudação é feita usuário toohello disponível como parte do fluxo de trabalho de saudação que é fornecido como uma entrada no fluxo de trabalho de registro de máquina hello. Isso autentica Olá máquina toosend dados de backup tooan identificado cofre em Olá serviço Backup do Azure.

credencial do cofre Olá é usado somente durante o fluxo de trabalho de registro de saudação. É tooensure de responsabilidade do usuário Olá que Olá as credenciais do cofre arquivo não seja comprometido. Se ela estiver em mãos Olá de qualquer usuário autorizado, o arquivo de credenciais de cofre Olá pode ser usado tooregister outras máquinas Olá mesmo cofre. No entanto, como dados de backup Olá são criptografados usando uma frase secreta que pertence o cliente toohello, dados de backup existentes não podem ser comprometidos. toomitigate essa preocupação, as credenciais do cofre são definidas tooexpire em 48hrs. Você pode baixar credenciais do cofre Olá de um cofre de backup a qualquer número de vezes – mas somente hello mais recente cofre credencial arquivo aplicável durante o fluxo de trabalho do hello registro.

### <a name="download-hello-vault-credential-file"></a>Baixe o arquivo de credencial de cofre Olá
arquivo de credencial de cofre Olá é baixado por meio de um canal seguro de saudação portal do Azure. Olá serviço Backup do Azure não tem conhecimento da chave privada de saudação do certificado de saudação e chave privada Olá não é mantido no portal de saudação ou serviço hello. Use Olá seguindo as etapas toodownload Olá cofre credencial arquivo tooa máquina local.

1. Entrar toohello [Portal de gerenciamento](https://manage.windowsazure.com/)
2. Clique em **dos serviços de recuperação** no painel de navegação esquerdo hello e selecione Olá Cofre de backup criado por você. Clique em Olá nuvem ícone tooget toohello exibição início rápido saudação do Cofre de backup.
   
   ![Visualização rápida](./media/backup-download-credentials/quickview.png)
3. Na página início rápido hello, clique em **baixar credenciais do cofre**. portal de Hello gera o arquivo de credencial do cofre hello, que fica disponível para download.
   
   ![Baixar](./media/backup-download-credentials/downloadvc.png)
4. portal de saudação irá gerar uma credencial do cofre usando uma combinação de nome do cofre hello e hello data atual. Clique em **salvar** toodownload Olá cofre credenciais toohello da conta local baixa a pasta ou selecione Salvar como do hello salvar menu toospecify um local para as credenciais do cofre hello.

### <a name="note"></a>Observação
* Certifique-se de que as credenciais do cofre Olá é salvo em um local que pode ser acessado em seu computador. Se ele estiver armazenado em um compartilhamento de arquivo/SMB, verifique as permissões de acesso de saudação.
* o arquivo de credenciais de cofre Olá é usado somente durante o fluxo de trabalho de registro de saudação.
* o arquivo de credenciais de cofre Olá expira após 48hrs e pode ser baixado do portal de saudação.
* Consulte toohello Backup do Azure [perguntas frequentes sobre](../articles/backup/backup-azure-backup-faq.md) para todas as questões sobre o fluxo de trabalho de saudação.

