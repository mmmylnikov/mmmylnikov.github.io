# Разметка Маркдаун
> Источник: https://guides.hexlet.io/markdown/

# Выделение текста

*Этот текст будет наклонным (курсив)*

_Этот текст будет наклонным (курсив)_

**Этот текст будет жирным**

__Этот текст будет жирным__

_Можно **вставлять** один тип в другой_

# Заголовки
```md
# Это самый крупный заголовок, он превращается в тег <h1>
## <h2>
### <h3>
#### <h4>
##### <h5>
###### <h6>
```
# Ссылки
```md
https://hexlet.io — текст простой ссылки станет кликабельной ссылкой автоматически

[Это ссылка на Хекслет](https://hexlet.io)
```

# Цитата
```md
> Это мудрая цитата
> Мудрого человека.
```
# Картинки
```md
![Это опциональный alt-текст](/assets/images/markdown/markdown.png)
```
# Код

```md
Для выделения кода (или любого неотформатированного текста) используются специальные символы — обратные тики: `

Иногда нужно добавить кусок кода `function(12);` в обычную строчку текста.

А иногда нужно вставить целый блок кода:

```javascript
const func = (num) => {
  if (num > 0) {
    return num - 1;
  }
  return num + 1;
};
\```
```


# Списки
Непронумерованный список:
```md
* Пункт
* Еще один пункт
  * Подпункт
  * Еще один подпункт
```
Пронумерованный список:
```md
1. Пункт
1. Еще один пункт
  1. Подпункт
  1. Еще один подпункт
```

# Из википедии
> Источник: https://en.wikipedia.org/wiki/Markdown
```md
Heading
=======

Sub-heading
-----------

Paragraphs are separated 
by a blank line.

Two spaces at the end of a line  
produce a line break.

Text attributes _italic_,
**bold**, `monospace`. Some implementations may use *single-asterisks* for italic text.

Horizontal rule:

---

Strikethrough:
~~strikethrough~~

Bullet list:

  * apples
  * oranges
  * pears

Numbered list:

  1. lather
  2. rinse
  3. repeat

An [example](http://example.com).

![Image](Icon-pictures.png "icon")

> Markdown uses email-style
> characters for blockquoting.
> Multiple paragraphs need to be prepended individually.

Basic inline <abbr title="Hypertext Markup Language">HTML</abbr> may be supported.
```