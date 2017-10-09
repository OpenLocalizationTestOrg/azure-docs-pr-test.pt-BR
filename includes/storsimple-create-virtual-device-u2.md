#### <a name="toocreate-a-virtual-device"></a>toocreate um dispositivo virtual
1. No portal do Azure de Olá, vá toohello **StorSimple Manager** serviço.
2. Vá toohello **dispositivos** página. Clique em **dispositivo virtual criar** final Olá Olá **dispositivos** página.
3. Em Olá **caixa de diálogo criar dispositivo Virtual**, especifique Olá detalhes a seguir.
   
    ![Dispositivo virtual de criação StorSimple](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nome** – um nome exclusivo para seu dispositivo virtual.
   2. **Modelo** -escolha o modelo de saudação do dispositivo virtual hello. Este campo só será exibido se você estiver executando a Atualização 2 ou posterior. Um modelo de dispositivo 8010 oferece 30 TB de armazenamento padrão enquanto 8020 tem 64 TB de armazenamento Premium. Especificar 8010
   3. cenários de recuperação de nível de item de toodeploy de backups. Selecione 8020 toodeploy alto desempenho, pouca cargas de trabalho de latência ou usado como um dispositivo secundário para recuperação de desastres.
   4. **Versão** -escolha versão de saudação do dispositivo virtual hello. Se um modelo de dispositivo 8020 for selecionado, em seguida, o campo de versão Olá não terá toohello usuário. Essa opção está ausente se todos Olá físico dispositivos registrados com esse serviço estão em execução no Update 1 (ou posterior). Este campo é apresentado somente se você tiver uma mistura de 1 de pré-atualização e atualização 1 em dispositivos físicos registrados com hello mesmo serviço. Fornecido Olá a versão do dispositivo virtual Olá determinará qual dispositivo físico você pode failover ou clone do, é importante que você crie uma versão apropriada do dispositivo virtual hello. Selecione:
      
      * Atualização 0.3 da versão, se você for realizar o failover ou DR de um dispositivo físico executando a Atualização 0.3 ou anterior. 
      * Atualização 1 da versão, se você for realizar o failover ou clonagem de um dispositivo físico executando a Atualização 1 (ou posterior). 
   5. **Rede virtual** – especifique uma rede virtual que você deseja toouse com este dispositivo virtual. Se usar o armazenamento Premium (atualização 2 ou posterior), você deve selecionar uma rede virtual que é compatível com hello conta de armazenamento Premium. redes virtuais Olá sem suporte ficará esmaecidas na lista suspensa de saudação. Você será avisado se você selecionar uma rede virtual sem suporte. 
   6. **Conta de armazenamento para a criação de dispositivo Virtual** – selecione uma imagem de saudação de toohold da conta de armazenamento do dispositivo virtual Olá durante o provisionamento. Esta conta de armazenamento deve estar no hello mesma região que o dispositivo virtual hello e rede virtual. Ele não deve ser usado para armazenamento de dados por Olá físico ou dispositivo virtual hello. Por padrão, uma nova conta de armazenamento será criada para essa finalidade. No entanto, se você souber que você já tem uma conta de armazenamento que é adequada para este uso, você pode selecioná-lo da lista de saudação. Se criar um dispositivo virtual premium, lista suspensa de saudação exibirá apenas contas de armazenamento Premium. 
      
      > [!NOTE]
      > dispositivo virtual Olá só pode funcionar com contas de armazenamento do Azure hello. Não há suporte para outros provedores de serviços de nuvem como Amazon, HP e OpenStack (que têm suporte para o dispositivo físico Olá) para o dispositivo virtual StorSimple hello.
      > 
      > 
   7. Clique em Olá tooindicate de marca de seleção que você entende que dados Olá armazenados no dispositivo virtual Olá serão hospedados em um datacenter da Microsoft. Quando você usa apenas um dispositivo físico, sua chave de criptografia é mantida com seu dispositivo; portanto, a Microsoft não pode descriptografá-la. 
      
       Quando você usa um dispositivo virtual, a chave de criptografia de saudação e a chave de descriptografia de saudação são armazenados no Microsoft Azure. Para saber mais, consulte [Considerações de segurança para usar um dispositivo virtual](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Clique em Olá seleção ícone toocreate Olá dispositivo virtual. dispositivo Olá pode levar cerca de 30 toobe minutos provisionado.
      
      ![Estágio de criação do dispositivo virtual StorSimple](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

