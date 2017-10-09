#### <a name="toocreate-a-cloud-appliance"></a>toocreate um dispositivo de nuvem

1. No portal do Azure de Olá, vá toohello **Gerenciador de dispositivos de StorSimple** service.
2. Vá toohello **dispositivos** folha. Na barra de comandos de saudação na folha de resumo de serviço hello, clique em **criar aplicativo de nuvem**.
    ![Criar dispositivo de nuvem StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. Em Olá **criar aplicativo de nuvem** folha, especifique Olá detalhes a seguir.
   
    ![Criar dispositivo de nuvem StorSimple](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nome** – Um nome exclusivo para seu dispositivo de nuvem.
   2. **Modelo** -escolha o modelo de saudação do dispositivo de nuvem hello. Um dispositivo 8010 oferece 30 TB de armazenamento padrão enquanto 8020 tem 64 TB de armazenamento Premium. Especifique 8010 cenários de recuperação de nível de item de toodeploy de backups. Selecione 8020 toodeploy alto desempenho, cargas de trabalho de baixa latência, ou use como um dispositivo secundário para recuperação de desastres.
   3. **Versão** -escolha Olá versão do dispositivo de nuvem hello. versão de Hello corresponde toohello versão da imagem de disco virtual Olá que é usado toocreate Olá nuvem dispositivo. Determinada versão de saudação da nuvem de saudação appliance determina quais físico dispositivo failover ou clonar no, é importante que você crie uma versão apropriada do dispositivo de saudação de nuvem.
   4. **Rede virtual** – especifique uma rede virtual que você deseja toouse com este dispositivo de nuvem. Se usar o armazenamento Premium, você deve selecionar uma rede virtual que é compatível com hello conta de armazenamento Premium. na lista suspensa de hello, redes virtuais Olá sem suporte estão esmaecidas. Você receberá um aviso se selecionar uma rede virtual sem suporte.
   5. **Subrede** -com base na rede virtual de saudação selecionado, lista suspensa de saudação exibe sub-redes Olá associado. Atribua um dispositivo de nuvem tooyour sub-rede.
   6. **Conta de armazenamento** – selecione uma imagem de saudação de toohold da conta de armazenamento do dispositivo de nuvem Olá durante o provisionamento. Esta conta de armazenamento deve estar no hello mesma região que o dispositivo de nuvem hello e rede virtual. Ele não deve ser usado para armazenamento de dados por Olá físico ou dispositivo de saudação de nuvem. Por padrão, uma nova conta de armazenamento é criada para essa finalidade. No entanto, se você souber que você já tem uma conta de armazenamento que é adequada para este uso, você pode selecioná-lo da lista de saudação. Se a criação de um dispositivo de nuvem premium, lista suspensa de saudação exibe apenas contas de armazenamento Premium.
      
      > [!NOTE]
      > dispositivo de nuvem Olá só pode funcionar com contas de armazenamento do Azure hello.
    
   7. Selecione Olá tooindicate de caixa de seleção que você entende que dados Olá armazenados no dispositivo de saudação de nuvem são hospedados em um datacenter da Microsoft.
       * Quando você usa apenas um dispositivo físico, sua chave de criptografia é mantida com seu dispositivo; portanto, a Microsoft não pode descriptografá-la.

       * Quando você usa um dispositivo de nuvem, a chave de criptografia de saudação e a chave de descriptografia de saudação são armazenados no Microsoft Azure. Para saber mais, consulte [Considerações de segurança para usar um dispositivo de nuvem](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Clique em **criar** appliance de nuvem tooprovision hello. dispositivo Olá pode levar cerca de 30 toobe minutos provisionado. Você será notificado quando o dispositivo de saudação de nuvem é criado com êxito. Vá tooDevices folha e lista de saudação de dispositivos atualizações appliance de nuvem toodisplay hello. status de saudação do dispositivo Olá é **pronto tooset backup**.
      
      ![Solução de nuvem StorSimple tooset de pronto para cima](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

