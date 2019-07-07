# jQuery 依然好用

前端发展虽然很快，现代浏览器原生 API 也已经足够好用了。同时由于 React、Angular、Vue 等框架的流行，直接操作 DOM 不再是好的模式。那么我们还要不要为了操作 DOM、Event 等再学习一下 jQuery 的 API。

我个人的做法是，学！ 青岛不倒我不倒...

这篇总结了日常 jQuery 的操作，和原生方法的替代。暂时只支持 IE10 以上的浏览器。当然 IE9、IE8 和以下这里暂不做总结。

## Query Selector

常用的 class、id 属性选择器都可以使用 `document.querySelector` 和 `document.querySelectorAll` 代替。区别是:

- `document.querySelector` 返回第一个匹配的 Element。
- `document.querySelectorAll` 返回所有匹配的 Element 组成的 NodeList。可以通过 `[].slice.call()` 转成 Array 数组。