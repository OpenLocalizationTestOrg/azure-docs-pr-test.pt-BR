<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake um backup

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Na listagem tabular de saudação de dispositivos, selecione e clique em seu dispositivo e, em seguida, clique em **todas as configurações**. Em Olá **configurações** folha, ir muito**Configurações > Gerenciar > política de Backup**.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. Em Olá **política de Backup** folha, clique em **+ adicionar política**.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. Em Olá **Criar política de backup** folha, forneça um nome que contenha entre 3 e 150 caracteres para sua política de backup.

4. Selecione Olá volumes toobe backup. Se você selecionar mais de um volume, esses volumes são toocreate agrupado junto um backup consistente.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. Na folha **Adicionar primeira agenda**:

    1. Selecione o tipo de saudação do backup. Para obter restaurações mais rápidas, selecione instantâneo **Local**. Para obter resiliência de dados, selecione instantâneo de **Nuvem**.
    2. Especifique a frequência de backup Olá em minutos, horas, dias ou semanas.
    3. Selecione um tempo de retenção. as escolhas de retenção de saudação dependem da frequência de backup hello. Por exemplo, para uma política diária, Olá retenção pode ser especificada em semanas, enquanto a retenção para uma política mensal será indicada em meses.
    4. Selecione Olá hora e data Olá política de backup.
    5. Clique em **Okey** toocreate política de backup hello.

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. Clique em **criar** toostart criação de política de backup de saudação. Você será notificado quando a política de backup Olá é criada com êxito. lista de saudação de políticas de backup também é atualizada.
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      Agora você tem uma política de backup que cria backups agendados de seus dados de volume.




