---
title: 'Подходы к реализации архитектуры: бессерверные приложения'
description: Общие сведения о подходах к реализации архитектуры для создания облачных корпоративных приложений — от n-уровневой архитектуры до бессерверных решений.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 74de96bef48f16ced4adf82855a740aa0afcdf1d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/14/2020
ms.locfileid: "72522897"
---
# <a name="architecture-approaches"></a>Подходы к архитектуре

Понимание имеющихся подходов к созданию архитектуры корпоративных приложений помогает прояснить роль, которую играют бессерверные приложения. Существует множество подходов и шаблонов, которые развивались в течение десятков лет разработки программного обеспечения. Каждый из них обладает своими достоинствами и недостатками. Во многих случаях окончательное решение может заключаться не в выборе одного подхода, а в объединении нескольких подходов. Сценарии миграции часто подразумевают переход от одного типа реализации архитектуры к другому с помощью гибридного подхода.

В этой главе представлен обзор как логических, так и физических шаблонов архитектуры для корпоративных приложений.

## <a name="architecture-patterns"></a>Шаблоны архитектуры

Современные бизнес-приложения используют различные шаблоны архитектуры. В этом разделе представлен обзор распространенных шаблонов. Перечисленные здесь шаблоны не обязательно являются рекомендуемыми. Они иллюстрируют различные подходы.

Дополнительные сведения см. в статье [Руководство по архитектуре приложений Azure](https://docs.microsoft.com/azure/architecture/guide/).

## <a name="monoliths"></a>Монолитные структуры

Многие бизнес-приложения используют шаблон монолита. Устаревшие приложения часто реализуются как монолитные. В шаблоне монолита все компоненты и операции с приложением содержатся в одном развертывании. Все, от пользовательского интерфейса до вызовов базы данных, включается в одну и ту же базу кода.

![Архитектура монолитных структур](./media/monolith-architecture.png)

У этого подхода есть несколько преимуществ. Часто извлечь одну базу кода и начать работу бывает легко. Время перехода к рабочей среде может быть меньше, а создание тестовых сред реализуется просто, как и предоставление новой копии. Монолит можно спроектировать таким образом, чтобы он включал в себя несколько компонентов и приложений.

К сожалению, при использовании шаблона монолита, как правило, требуется разделение при масштабировании. К основным недостаткам монолитного подхода относятся следующие:

- Работать параллельно в одной базе кода довольно трудно.
- Любое изменение, каким бы простым оно ни было, требует развертывания новой версии всего приложения.
- Рефакторинг потенциально влияет на все приложение.
- Часто единственным решением для масштабирования является создание нескольких ресурсоемких копий монолитных ресурсов.
- По мере расширения систем или приобретения других систем интеграция может быть затруднительной.
- Тестирование может быть затруднено из-за необходимости настройки всего монолита.
- Повторное использование кода является сложной задачей, и часто другие приложения в конечном итоге имеют собственные копии кода.

Многие компании рассматривают облако как возможность миграции монолитных приложений, а также их рефакторинга на более удобные шаблоны. Общепринятой практикой является разбиение отдельных приложений и компонентов, чтобы они поддерживались, развертывались и масштабировались отдельно.

## <a name="n-layer-applications"></a>N-уровневые приложения

N-уровневое приложение разделяет логику приложения на определенные слои, наиболее распространенные из которых:

- Пользовательский интерфейс
- бизнес-логика;
- Доступ к данным

Другие слои могут включать в себя ПО промежуточного слоя, пакетную обработку и API. Важно отметить, что слои являются логическими. Хотя они разрабатываются изолированно, их можно развернуть на одной целевой платформе.

![N-уровневая архитектура](./media/n-layer-architecture.png)

У подхода n-уровневой архитектуры есть несколько преимуществ:

- Рефакторинг выполняется изолированно для слоя.
- Команды могут независимо создавать, тестировать, развертывать и обслуживать отдельные слои.
- Слои можно переключать, например, уровень данных может обращаться к нескольким базам данных без необходимости внесения изменений в слой пользовательского интерфейса.

Бессерверный интерфейс можно использовать для реализации одного или нескольких уровней.

## <a name="microservices"></a>Микрослужбы

Архитектуры с **[микрослужбами](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)** обладают следующими общими характеристиками:

- Приложения состоят из нескольких небольших служб.
- Каждая служба работает в своем собственном процессе.
- Службы согласовываются с предметными областями бизнеса.
- Службы обмениваются данными через упрощенные API, обычно используя HTTP в качестве транспортного протокола.
- Службы можно развертывать и обновлять независимо друг от друга.
- Службы не зависят от одного хранилища данных.
- Система разработана с учетом сбоев, и приложение может работать даже в случае сбоя определенных служб.

Микрослужбы не обязательно должны быть взаимоисключающими по отношению к другим подходам к архитектуре. Например, n-уровневая архитектура может использовать микрослужбы для среднего уровня. Микрослужбы также можно реализовать различными способами — от виртуальных каталогов на узлах IIS до контейнеров. Благодаря характеристикам микрослужб они практически идеальны для бессерверных реализаций.

![Архитектура микрослужб](./media/microservices-architecture.png)

Архитектуры с микрослужбами обладают следующими преимуществами:

- Рефакторинг часто выполняется только для одной службы.
- Службы можно обновлять независимо друг от друга.
- Устойчивость и эластичность можно настроить в соответствии с требованиями отдельных служб.
- Разработка может выполняться параллельно различными командами на разных платформах.
- Проще писать комплексные тесты для изолированных служб.

Микрослужбы имеют свои собственные сложности, в том числе:

- Определение доступных служб и способа их вызова.
- Управление жизненным циклом служб.
- Необходимость понимания того, как службы объединяются в общем приложении.
- Требуется полное системное тестирование вызовов, выполненных в разнородных службах.

Существуют решения для устранения всех этих проблем, включая использование преимуществ бессерверной архитектуры, которые будут рассмотрены позже.

>[!div class="step-by-step"]
>[Назад](index.md)
>[Вперед](architecture-deployment-approaches.md)
