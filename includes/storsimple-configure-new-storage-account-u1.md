<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd uma conta de armazenamento StorSimple 8000 Series atualização 1.0
1. O serviço de Gerenciador do StorSimple Olá página inicial, selecione seu serviço e clique duas vezes nele. Isso o levará toohello **início rápido** página. Selecione Olá **configurar** página.
2. Clique em **Adicionar/editar conta de armazenamento**.
3. Em Olá **Adicionar/Editar conta de armazenamento** caixa de diálogo, clique em **adicionar novo**.
4. Em Olá **provedor** provedor de serviços de nuvem apropriado do campo, selecione hello. provedores de saudação com suporte são Azure, Amazon S3, Amazon S3 com RRS, HP e OpenStack. Especifica credenciais de saudação e local de saudação associado à conta de armazenamento de saudação de seus provedores de serviço de nuvem. campos de Olá apresentados credenciais serão diferentes dependendo de provedor de serviços de nuvem Olá especificado. 
   
   * Se você selecionou o Azure como seu provedor de serviços de nuvem, fornecer Olá **nome** e hello primário **chave de acesso** para sua conta de armazenamento do Microsoft Azure. Para uma conta do Azure, local hello será preenchido automaticamente.
     
        ![Adicionar Conta de armazenamento do Azure](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Se você tiver selecionado Amazon S3 ou Amazon S3 com RRS, forneça um **Nome de Conta de Armazenamento** amigável, uma **Chave de Acesso** e uma **Chave Secreta**. Para Amazon S3 e Amazon S3 com RRS, Olá locais a seguir têm suporte:
     
     * Padrão dos EUA
     * Oeste dos EUA (Oregon)
     * Oeste dos EUA (Norte da Califórnia)
     * UE (Irlanda)
     * Pacífico Asiático (Cingapura)
     * Pacífico Asiático (Sydney)
     * Pacífico Asiático (Tóquio)
     * América do Sul (São Paulo)
       
       ![Adicionar Conta de armazenamento do Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * Se você tiver selecionado HP como seu provedor de serviços de nuvem, forneça um **Nome de Conta de Armazenamento** amigável, uma **ID de Locatário**, um **Nome de Usuário** e uma **Senha**. Para o HP, Olá locais a seguir têm suporte:
     
     * Leste dos EUA
     * Oeste dos EUA
       
       ![Adicionar uma conta de armazenamento HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Se você tiver selecionado **Openstack** como seu provedor de serviços de nuvem, forneça um **Nome de Host**, uma **Chave de Acesso** e uma **Chave Secreta**.
     
     > [!NOTE]
     > Para todos os provedores de serviço nuvem hello, excluindo o Azure, um nome amigável é permitido. Você pode usar diferentes nomes amigáveis e criar mais de uma conta de armazenamento com o mesmo conjunto de credenciais de saudação.
     > 
     > 
     
        ![Adicionar conta de armazenamento Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Selecione **habilitar o modo SSL** toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello. Olá limpar **habilitar o modo SSL** caixa de seleção somente se você estiver operando em uma nuvem privada.
   
   > [!NOTE]
   > Se você estiver usando o HP como seu provedor, SSL sempre estará habilitado.
   > 
   > 
6. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Você será notificado depois da conta de armazenamento Olá é criada com êxito.
7. Olá recentemente criado a conta de armazenamento será exibido na Olá **configurar** página em **contas de armazenamento**. Clique em **salvar** toosave Olá nova conta de armazenamento. Clique em **OK** quando solicitado para confirmar.

