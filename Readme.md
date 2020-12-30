# OBSOLETE - How to extend the SlideOutLayout and create a custom CommandManager

<p><strong>This example is OBSOLETE. The approach described here cannot be used in version 13.2 and older. At the moment, there is no alternative solution. <br /><br /><br />[Old content]</strong><br />This example demonstrates how to add one more List to the SlideOutLayout and divide commands into two groups.</p>
<p>The first thing to do is create a copy of the SlideOutLayout.hml file, and add one more List to it. Actually, you only need to create a copy of the existing list. Then, create a CSS rule for the second List to always keep it on the bottom edge and one more CSS rule for the partial view that contains both Lists:</p>


```css
.layout-list-bottom {
    position: absolute;
    bottom: 0;
    height: auto;
    width: 100%;
}
.nav-list {
    height: 100%;
}



```


<p>Create a separate file (CustomLayout.css, for example) and put the code above into this file. In addition, change the data-dx-command-container attribute of each dxList, so it define a custom location. The default location name is "navigation", but we will use "navigationTop" and "navigationBottom" names to help the CommandManager to find an appropriate container.</p>


```html
<div class="nav-patrial-view" data-options="dxView : { name: 'custom-nav-list' } " >
    <div data-bind="dxList: {}" style="height: 100%" data-options="dxCommandContainer : { locations: [{'name':'navigationTop'}] } " >
        <div data-bind="visible: visible, css: { 'dx-state-disabled': disabled }" data-options="dxTemplate : { name: 'item' } " >
            <div data-bind="click: clickAction">
                <!-- ko if: icon -->
                <span  data-bind="attr: { 'class': 'dx-icon dx-icon-' + icon }"></span>
                <!-- /ko -->
                <!-- ko if: iconSrc -->
                <img class="dx-icon" data-bind="attr: { src: iconSrc }" />
                <!-- /ko -->
                <div class="dx-navigation-item" data-bind="text: title"></div>
            </div>
        </div>
    </div>
    <div data-bind="dxList: {}" class="layout-list-bottom" data-options="dxCommandContainer : { locations: [{'name':'navigationBottom'}] } " >
        <div data-bind="visible: visible, css: { 'dx-state-disabled': disabled }" data-options="dxTemplate : { name: 'item' } " >
            <div data-bind="click: clickAction">
                <!-- ko if: icon -->
                <span  data-bind="attr: { 'class': 'dx-icon dx-icon-' + icon }"></span>
                <!-- /ko -->
                <!-- ko if: iconSrc -->
                <img class="dx-icon" data-bind="attr: { src: iconSrc }" />
                <!-- /ko -->
                <div class="dx-navigation-item" data-bind="text: title"></div>
            </div>
        </div>
    </div>
</div>


```


<p>Now, all that you need is to specify an appropriate location for commands:</p>


```js
"navigation": [
    {
        title: "Index",
        action: "#Index",
        icon: "home",
        location: "navigationTop"
    },
    {
        title: "About",
        action: "#About",
        icon: "info",
        location: "navigationBottom"
    }
]

```



<br/>


