---
title: Доступный компонент «из коробки»
date: 2021-11-18
author: nikita-dubko
editors:
    - vadim-makeev
tags:
    - a11y
preview: Небольшое руководство по созданию доступного компонента сразу, без необходимости переделывания.
---

Недавно коллеги попросили меня собрать небольшой чек-лист создания доступного компонента «из коробки». Постарался преобразовать свой опыт в простое руководство, следуя которому проще не переделывать компонент, когда будет нужно чинить недоступное, а сразу делать хорошо.

## Зачем мне делать что-то доступным?

У вас идеальное зрение? У вас всегда оно будет таким?

Ломали ли вы когда-нибудь руку? Или, может, получали вывих? Возможно, по неосторожности порезали палец? Удобно было пользоваться интернетом одной рукой?

Ломалась ли у вас мышка? Или тачпад? Представьте, что у вас сломался тачпад, при этом вам срочно надо найти сервис для его ремонта, но телефон разряжен, а поисковик сделан так, что с клавиатуры вы не можете перейти по ссылке. Удачи и терпения!

Мы, разработчики, всё ещё не умеем считать упущенную выгоду. Как на одной из конференций сказал [Анатолий Попко](http://adpopko.ru/) (незрячий эксперт в сфере невизуальной доступности), он готов тратить деньги в различных сервисах, чтобы вести свой бизнес. Но многие сервисы почему-то не хотят принимать его деньги, не давая пользоваться функциями полноценно.

Делая удобные интерфейсы для людей с особыми возможностями, вы делаете очень удобные интерфейсы для самих себя.

## Как люди могут пользоваться вашим сайтом?

Есть много способов пользоваться сайтами помимо классического сёрфинга по интернету с монитором, мышкой и клавиатурой.

- _Со скринридером —_ сайт озвучивается. Полезно незрячим людям.
- _С клавиатуры —_ когда есть возможность пользоваться навигацией без мышки, кнопками <kbd>Tab</kbd>, <kbd>Enter</kbd>, <kbd>Space</kbd> и стрелками. Полезно людям с ограничениями опорно-двигательного аппарата и тем, кто не хочет тянуться к мышке.
- _Мышкой —_ когда нет возможности пользоваться клавиатурой.
- _С включённым зумом —_ потому что ослабленное зрение.
- _С включённым контрастом —_ потому что изначальный контраст не подходит. Полезно людям с цветовой слепотой.
- _С выключенной анимацией —_ потому что мельтешение вредит. Полезно людям с эпилепсией.
- _Левой рукой —_ потому что так удобнее. Полезно левшам.

## Как сразу создавать доступные компоненты?

1. **Делайте по готовым инструкциям,** не мудрите. До вас уже многое придумано, и придумано хорошо. На Smashing Magazine есть [отличный гайд по теме](https://www.smashingmagazine.com/2021/03/complete-guide-accessible-front-end-components/).

2. **Верстайте семантично —** тогда скринридер сможет большую часть задач решить сам, без сложностей со стороны разработки.

3. **Используйте [ARIA](https://www.w3.org/WAI/standards-guidelines/aria/),** если семантики не хватает. Но сначала всё же постарайтесь справиться в пункте № 2.

4. **Мелкие кликабельные области — плохо.** Попробуйте своим пальцем попасть на тачах в мелкую кнопку, чтобы закрыть какой-нибудь попап, перекрывающий контент. Бесит? Придерживайтесь минимума в 44 пикселя для меньшей стороны интерактивного блока — этого обычно достаточно для пальца.

5. **Внутри ссылок `<a>` должен быть текст,** иначе скринридер постарается прочитать `href` ссылки. Вряд ли у вас все адреса на странице красивые и понятные. Нет текста по дизайну — добавьте `<span class="visibility-hidden">`. А лучше пообщайтесь с дизайнером, договоритесь с ним, какой можно добавить текст.

6. **Не путайте кнопки и ссылки:** переход в восстанавливаемое по URL состояние? Это ссылка `<a>`. Нет перехода? Кнопка `<button>`.

7. **Не используйте только иконки для подписи интерактивных элементов.** Пусть это будет текст, не только иконка. Добавьте скрытый `span` или примените `aria-label`. По иконке и зрячие не всегда поймут, что хотел сказать автор. Текст универсален для носителей языка.

8. **Подписывайте картинки.** Люди без зрения тоже хотят понимать, что там. Не можете подписать — поставьте пустой `alt=""`, иначе скринридер постарается прочитать URL картинки. Если у вас настроена раздача статики с CDN, то адреса картинок будут не самые красивые и понятные.

9. **Не прячьте визуальный фокус.** Если нужно спрятать «некрасивый» дефолтный фокус, оформите кастомный. Объясните дизайнеру, что прятать нельзя. Если он против, попросите его добавить `cursor: none` в его графический редактор для большей наглядности проблемы.

10. **Захватывайте фокус в модальных окнах.** Фокус не должен проваливаться за пределы модалки.

11. **Переносите фокус при открытии модального окна или всплывашки внутрь.** Так удобнее, можно сразу начать навигироваться по полезному контенту, а не искать его при помощи клавиши <kbd>Tab</kbd>.

12. **Верните фокус обратно к кнопке,** которая открыла модальное окно, после того, как оно закроется.

13. **Цвета должны различаться** сильно, если они играют роль. Лучше помимо цвета использовать ещё и иконки, подчёркивания, отличающийся текст. Зелёный цвет для обозначения успеха и красный цвет для ошибки некоторые видят как _одинаковый_ для _непонятно-чего._ К тому же, если ваш сайт активно использует красный цвет как брендовый, он не будет выглядеть как состояние ошибки.

14. **Для видео используйте субтитры,** которые не вшиты в видео. Вшитые субтитры невозможно перевести и прочитать скринридером.

15. **Используйте медиафичи `prefers-*`,** которые подхватывают настройки операционной системы. Например, `prefers-reduced-motion` или `prefers-contrast`. Если пользователь поставил такую настройку, у него есть на это причины.

16. **Не используйте мелкий шрифт,** он бесит даже людей с идеальным зрением. Я, например, мелкий шрифт не вижу. Дизайнер говорит, что так надо? Попросите его выставить в графическом редакторе `font-size: 5px !important`, чтобы лучше продемонстрировать проблему.

17. **Не переусердствуйте.** Делать идеальную доступность нет смысла, пока не работают основные сценарии. Нужно делать хорошо и дать возможность пользоваться важными сценариями сайта. Когда кнопка «Купить» в интернет-магазине не работает, идеальные подписи к картинкам бессмысленны.

18. **Используйте правильные тексты.** Не пишите на кнопке «Кнопка», роль элемента и так читается скринридером. Он умеет зачитывать роли для списков, кнопок, ссылок, навигации и других элементов.

## Дополнительные материалы

- [Как незрячий пользуется iPhone, MacBook и Apple Watch](https://youtu.be/RQiN1Hhrxu0).
- [Пандус для сайта](https://habr.com/ru/company/linka/blog/346238/).