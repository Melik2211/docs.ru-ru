---
title: Настройка поддержки транзакций WS-Atomic
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF], configuring WS-Atomic Transaction
ms.assetid: cb9f1c9c-1439-4172-b9bc-b01c3e09ac48
ms.openlocfilehash: 6399d64746db158ba0569eaf0137127603973513
ms.sourcegitcommit: cdf5084648bf5e77970cbfeaa23f1cab3e6e234e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "76919347"
---
# <a name="configure-ws-atomic-transaction-support"></a>Настройка поддержки WS-Atomic Transaction

В этой теме описывается, как можно настроить поддержку WS-AtomicTransaction (WS-AT) с помощью программы конфигурации WS-AT.

## <a name="use-the-ws-at-configuration-utility"></a>Использование служебной программы настройки WS-AT

Программа конфигурации WS-AT (wsatConfig.exe) используется для настройки параметров WS-AT. Чтобы включить службу протокола WS-AT, с помощью программы конфигурации следует настроить порт HTTPS для WS-AT, привязать сертификат X.509 к порту HTTPS и настроить сертификаты авторизованных партнеров, указав имена субъектов сертификатов или отпечатки. Программа конфигурации также позволяет выбрать режим трассировки и задать значения времени ожидания по умолчанию для исходящих и максимальных входящих транзакций.

Функциями этой программы можно воспользоваться с помощью оснастки страницы свойств консоли управления (MMC) в консоли управления службами компонентов или с помощью окна командной строки. Настройте поддержку WS-AT на локальном компьютере с помощью окна командной строки; задайте параметры на локальных и удаленных компьютерах с помощью оснастки MMC.

Окно командной строки можно открыть в папке установки Windows SDK "%WINDIR%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation".

Дополнительные сведения о программе командной строки см. в разделе [служебная программа настройки WS-AtomicTransaction (WsatConfig. exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md).

Если вы используете Windows XP или Windows Server 2003, доступ к оснастке MMC можно получить, перейдя в раздел **Панель управления/Администрирование/службы компонентов**, щелкнув правой кнопкой мыши **Мой компьютер**и выбрав пункт **Свойства**. Здесь же можно настроить координатор распределенных транзакций (Майкрософт). Параметры, доступные для конфигурации, группируются на вкладке **WS-AT** . Если вы используете Windows Vista или Windows Server 2008, оснастку MMC можно найти, нажав кнопку **Пуск** и введя `dcomcnfg.exe` в поле **поиска** . Когда откроется консоль MMC, перейдите к узлу **Мои Компутер\дистрибутед Transaction КУРДИНАТОР\ЛОКАЛ DTC** , щелкните правой кнопкой мыши и выберите пункт **свойства**. Параметры, доступные для конфигурации, группируются на вкладке **WS-AT** .

Дополнительные сведения об оснастке см. в разделе [оснастка MMC "Настройка WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)".

Для работы с пользовательским интерфейсом средства необходимо зарегистрировать файл WsatUI.dll. Путь к этому файлу:

%PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin

Чтобы зарегистрировать продукт, выполните следующую команду в окне командной строки:

`regasm.exe /codebase WsatUI.dll`

## <a name="enable-ws-at"></a>Включить WS-AT

Чтобы включить службу протокола WS-AT в MSDTC с использованием порта 443 и сертификата X.509 с закрытым ключом, установленным в хранилище локального компьютера, используйте средство wsatConfig.exe со следующей командой.

`WsatConfig.exe –network:enable –port:8443 –endpointCert:<machine|"Issuer\SubjectName"> -accountsCerts:<thumbprint|"Issuer\SubjectName"> -restart`

Замените соответствующие параметры значениями, подходящими для вашей среды.

Чтобы выключить службу протокола WS-AT в MSDTC, используйте средство wsatConfig.exe со следующей командой.

`WsatConfig.exe –network:disable -restart`

## <a name="configure-trust-between-two-machines"></a>Настройка отношений доверия между двумя компьютерами

Для службы протокола WS-AT требуется, чтобы администратор явно авторизовал отдельные учетные записи для их участия в распределенных транзакциях. Администратор двух компьютеров может настроить оба из них, чтобы они установили взаимно доверенные отношения путем обмена правильным набором сертификатов между компьютерами, их установки в соответствующие хранилища сертификатов и использования средства wsatConfig.exe для добавления сертификата каждого компьютера в список сертификатов авторизованных участников другого компьютера. Эта процедура необходима для выполнения распределенных транзакций между двумя компьютерами с WS-AT.

В следующем примере описываются этапы установления доверия между двумя компьютерами, A и B.

### <a name="create-and-export-certificates"></a>Создание и экспорт сертификатов

Для этой процедуры требуется оснастка диспетчера сертификатов MMC. Чтобы открыть эту оснастку, выберите меню «Пуск - Выполнить», введите «mmc» в поле ввода и нажмите кнопку «ОК». Затем в окне **Консоль1** перейдите к оснастке **файл/добавить-удалить** , нажмите кнопку Добавить и выберите **Сертификаты** из **доступного автономного списка оснастки** . Наконец, выберите **учетную запись компьютера** для управления и нажмите кнопку **ОК**. Узел **Сертификаты** отображается в консоли оснастки.

Чтобы установить доверенные отношения, необходимо уже иметь в наличии необходимые сертификаты. Сведения о создании и установке новых сертификатов перед выполнением следующих шагов см. в разделе [как создавать и устанавливать временные сертификаты клиентов в WCF во время разработки](https://docs.microsoft.com/previous-versions/msp-n-p/ff650751(v=pandp.10)).

1. На компьютере A, использующем оснастку диспетчера сертификатов MMC, импортируйте существующий сертификат (certA) в хранилище LocalMachine\MY (Личный узел) и LocalMachine\ROOT (узел доверенного корневого центра сертификации). Чтобы импортировать сертификат на конкретный узел, щелкните узел правой кнопкой мыши и выберите **все задачи/импорт**.

2. На компьютере B, использующем оснастку диспетчера сертификатов MMC, создайте или получите сертификат (certB) с закрытым ключом и импортируйте его в хранилище LocalMachine\MY (личный узел) и LocalMachine\ROOT (узел доверенного корневого центра сертификации).

3. Экспортируйте открытый ключ certA в файл, если это еще не сделано.

4. Экспортируйте открытый ключ certB в файл, если это еще не сделано.

### <a name="establish-mutual-trust-between-machines"></a>Установка взаимного доверия между компьютерами

1. На компьютере A импортируйте файловое представление certB в хранилища LocalMachine\MY и LocalMachine\ROOT. Это объявляет, что компьютер A доверяет certB связываться с ним.

2. На компьютере B импортируйте файл certA в хранилища LocalMachine\MY и LocalMachine\ROOT. Это подразумевает, что компьютер B доверяет certA связываться с ним.

По завершении этих этапов между двумя компьютерами устанавливаются отношения доверия, и их можно настроить таким образом, чтобы они связывались друг с другом с использованием WS-AT.

### <a name="configure-msdtc-to-use-certificates"></a>Настройка MSDTC для использования сертификатов

Поскольку служба протокола WS-AT работает как клиент и как сервер, она должна прослушивать входящие подключения и инициировать исходящие. Поэтому координатор MSDTC необходимо настроить таким образом, чтобы он знал, какой сертификат использовать для связи с внешними сторонами, а какие авторизовывать во время приема входящего подключения.

Это можно осуществить с помощью оснастки MMC WS-AT. Дополнительные сведения об этом средстве см. в разделе [оснастка конфигурации WS-ATOMICTRANSACTION MMC](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md) . Далее описывается, как устанавливать отношения доверия между двумя компьютерами с MSDTC.

1. Задайте параметры компьютера A. Для "сертификат конечной точки" выберите Cert a. Для "полномочные сертификаты" выберите Цертб.

2. Задайте параметры компьютера B. В качестве "сертификата конечной точки" выберите Цертб. Для "полномочные сертификаты" выберите сертификат а.

> [!NOTE]
> Когда один компьютер отправляет сообщение другому, отправитель пытается проверить совпадение имени субъекта сертификата получателя и имени компьютера получателя. Если они не совпадают, проверка сертификата завершается ошибкой и оба компьютера не могут связываться друг с другом.
>
> Для компьютера, входящего в состав домена, имя представляет собой полное доменное имя. По умолчанию имя компьютера в рабочей группе является именем NetBIOS компьютера. Однако имя также может содержать суффикс службы доменных имен (DNS), если он используется для подключения между двумя компьютерами.
>
> Если имя компьютера меняется, например, когда компьютер рабочей группы входит в состав домена, необходимо повторно выдать сертификаты или вручную настроить суффиксы DNS.

## <a name="security"></a>по безопасности

Поскольку некоторые параметры, относящиеся к MSDTC и WS-AT, хранятся в реестре в разделе HKLM\Software\Microsoft\MSDTC и HKLM\Software\Microsoft\WSAT соответственно, убедитесь, что эти ключи реестра защищены и только администраторы могут указывать в них значения. В редакторе реестра щелкните правой кнопкой мыши ключ, который необходимо защитить, и выберите **разрешение** на установку соответствующего элемента управления доступом. Для обеспечения безопасности и целостности системы крайне важно, чтобы для важных ключей был задан атрибут «только для чтения» для пользователей с ограниченными правами доступа.

При развертывании MSDTC администратор должен обеспечить безопасность обмена любыми данными MSDTC. При развертывании рабочей группы изолируйте инфраструктуру транзакций от злоумышленников. При кластерном развертывании защитите реестр кластера.

## <a name="tracing"></a>Трассировка

Служба протокола WS-AT поддерживает интегрированную трассировку, зависящую от транзакций, которая может быть включена и управляться с помощью средства [оснастки MMC "Настройка конфигурации WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md) ". Трассировки могут включать в себя данные, указывающие на время создания зачисления для определенной транзакции, время достижения транзакцией конечного состояния и результат, полученный зачислением каждой транзакции. Просмотреть все трассировки можно с помощью средства [Service Trace Viewer (SvcTraceViewer. exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) .

Служба протокола WS-AT также поддерживает интегрированную трассировку ServiceModel во время сеанса трассировки ETW. Результатом этого являются более подробные трассировки, относящиеся к связи, в дополнение к существующим трассировкам транзакций.  Чтобы включить такие дополнительные трассировки, выполните следующие действия.

1. Откройте меню **Пуск/выполнить** , введите "regedit" в поле "вход" и нажмите кнопку **ОК**.

2. В **редакторе реестра**перейдите к следующей папке в левой области, Hkey_Local_Machine \software\microsoft\wsat\3.0\

3. Щелкните правой кнопкой мыши значение `ServiceModelDiagnosticTracing` на правой панели и выберите **изменить**.

4. В поле Ввод **данных значения** введите одно из следующих допустимых значений, чтобы указать уровень трассировки, который требуется включить.

- 0: выключено

- 1: критично

- 3: ошибка. Это значение по умолчанию

- 7: предупреждение

- 15: информация

- 31: подробно

## <a name="see-also"></a>См. также:

- [Служебная программа конфигурации WS-AtomicTransaction (wsatConfig.exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [Оснастка консоли MMC для конфигурации WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)
