---
prev: ./
next: ./misc
sidebarDepth: 2
---

# Компоненты приложения

::: details Таблица содержания
[[toc]]
:::

## Что такое компоненты приложения?
Активити, службы, широковещательные приемники (также известные как приемники) и поставщики контента (также известные как поставщики) вместе называются компонентами приложения. Технически, все они наследуют класс `ComponentInfo`.

## Почему компоненты, заблокированные с помощью AM, не распознаются другими связанными приложениями?
Это происходит из-за используемого мной метода блокировки. Этот метод называется [Intent Firewall][1] (IFW) и он совместим с [Watt][2] и [Blocker][3]. [MyAndroidTool][4] (MAT) поддерживает IFW, но использует другой формат. Существуют и другие методы блокировки компонентов приложения, например _pm_ и [Shizuku][5]. Если компонент приложения заблокирован с помощью этих последних методов, уязвимое приложение может идентифицировать его и разблокировать, поскольку оно имеет полный доступ к своим собственным компонентам. Множество мошеннические приложения на самом деле пользуются этим, чтобы разблокировать компоненты трекера.

## Сохраняются ли в AM компоненты приложения, заблокированные другими инструментами?
**Нет.** Но компоненты, заблокированные системой Android или любыми другими инструментами, отображаются на странице [«Сведения о приложении»][10] (во вкладке компонентов). Начиная с версии 2.5.12, вы можете импортировать эти правила в [настройках приложения][9]. Но поскольку нет возможности отличить компоненты, заблокированные сторонними приложениями, от компонентов, заблокированных системой, вы должны быть очень осторожны при выборе приложения.

## Что бывает с компонентами, заблокированными с помощью AM, которые также заблокированы другими инструментами?
AM снова блокирует компоненты, используя [Intent Firewall][1] (IFW). Они не разблокируются (если заблокированы с помощью метода _pm_ или [Shizuku][5]) и снова блокируются. Но если вы разблокируете компонент на странице [«Сведения о приложении»][6], он будет возвращен в состояние по умолчанию - заблокирован или разблокирован, как описано в соответствующем манифесте приложения - с использованием как IFW, так и метода _pm_. Однако компоненты, заблокированные с помощью [MyAndroidTools][4] (MAT) с методом IFW не будет разблокирован AM. Чтобы решить эту проблему, вы можете сначала импортировать соответствующую конфигурацию в [настройках AM][9]. В этом случае конфигурации MAT будут удалены. Однако эта опция доступна только с версии 2.5.12.

## Что такое глобальная блокировка компонентов?
Когда вы блокируете компонент на странице [«Сведения о приложении»][6], блокировка по умолчанию не применяется. Применяется она только тогда, когда вы применяете блокировку с помощью опции _«Применить правила»_ в правом верхнем меню. Если вы включите _глобальную блокировку компонентов_, блокировка будет применена, как только вы заблокируете компонент. Однако если вы решите заблокировать трекеры, блокировка применится автоматически независимо от этого параметра. Вы также можете снять блокировку приложения, просто нажав на _«Удалить правила»_ в том же меню на странице **«Сведения о приложении»**. Поскольку поведение по умолчанию дает вам больший контроль над приложениями, лучше оставить опцию _глобальной блокировки компонентов_ выключенной.

_Смотрите также: [Глобальная блокировка компонентов][7]_

## Как разблокировать компоненты трекера, заблокированные с помощью операций в один клик или пакетных операций?
Некоторые приложения могут работать некорректно из-за их зависимости от компонентов трекера, заблокированных с помощью AM. Начиная с версии 2.5.12, есть возможность разблокировать компоненты трекеров на странице [«Операции в один клик»][8]. Однако в предыдущих версиях таких опций нет. Чтобы разблокировать этот трекер, сначала перейдите на страницу [«Сведения о приложении»][6] некорректного приложения. Затем, переключившись на вкладку _«Активити»_, нажмите на опцию _«Удалить правила»_ в правом верхнем меню. Все правила блокировки, относящиеся к компонентам приложения, будут немедленно удалены. В качестве альтернативы, если вы нашли компонент, вызывающий проблему, вы можете разблокировать компонент, нажав на кнопку _«разблокировать»_ рядом с названием компонента. Если вы включили _глобальную блокировку компонентов_ в настройках приложения, сначала отключите ее, так как опция _«Удалить правила»_ не будет отображаться, когда блокировка включена.

Если на вашем устройстве установлены **Сервисы Google Play** (`com.google.android.gms`), разблокировка следующих [сервисов][services] может решить проблему:
- **Ad Request Broker Service**<br /> `.ads.AdRequestBrokerService`
- **Cache Broker Service**<br /> `.ads.cache.CacheBrokerService`
- **Gservices Value Broker Service**<br /> `.ads.GservicesValueBrokerService`
- **Служба уведомления об идентификаторах рекламы**<br /> `.ads.identifier.service.AdvertisingIdNotificationService`
- **Служба рекламного идентификатора**<br /> `.ads.identifier.service.AdvertisingIdService`

[1]: https://carteryagemann.com/pages/android-intent-firewall.html
[2]: https://github.com/tuyafeng/Watt
[3]: https://github.com/lihenggui/blocker
[4]: https://www.myandroidtools.com
[5]: https://github.com/RikkaApps/Shizuku
[6]: ../guide/app-details-page.md
[7]: ../guide/settings-page.md#гnобаnьная-бnокировка-компонентов
[8]: ../guide/one-click-ops-page.md
[9]: ../guide/settings-page.md#импортирование-существующих-правиn
[10]: ../guide/app-details-page.md#цветовые-коды
[services]: ../guide/app-details-page.md#сnужбы
