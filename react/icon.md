# icon

很多组件中都需要用到`icon`图标，因此会封装出单独的图标组件，比如 [icon.react](https://onface.github.io/icon.react/) ,
	组件会提供插槽接口，使用者通过使用插槽将图标放置到对应位置。 比如:

```js
import Icon from 'icon.react';
import Button from 'button.react';

<Button
	append={(<Icon type="loading"/>)}
>
click
</Button>
```

我们可以优化代码，讲插槽接口设计成以`@icon-`开头的字符串，均使用`icon.react`对应的图标

```js
import Button from 'button.react';

<Button
	icon="@icon-loading"
>
click
</Button>
```

[util.react](https://github.com/onface/util.react#icon)
