# ff-url-finder

Экспортирует класс `URLFinder`.

Конструктор: `new URLFinder(tlDomains, localDomains)`, где _tlDomains_ — массив доменов 1-го уровня, которые должны распознаваться без явного указания протокола,
_localDomains_ — массив доменов, ссылки в которых считаются локальными.

Метод: `parse(text)` — разбивает строку текста на список блоков следующих типов:

````
{type: "text", text: "aa "} // простой текст
{type: "link", text: "google.com", url: "http://google.com/"} // внешняя ссылка
{type: "atLink", text: "@alice", username: "alice"} // @-ссылка с username
{type: "localLink", text: "freefeed.net/abc", uri: "/abc"} // локальная ссылка (в одном из доменов localDomains)
{type: "email", text: "aa@bb.ru", address: "aa@bb.ru"} // адрес e-mail
````
Везде: _type_ — тип блока, _text_ — текст, который должен показываться пользователю (текст внутри <a> для ссылок). Остальные поля типо-специфичны.

## Фичи

* Понимает ссылки без явно указанного протокола (для заданного набора TLD);
* В тексте для пользователя делает urldecode, а также преобразует IDN к человекопонятному виду;
* Правильно обрабатывает концевые скобки в URL.
