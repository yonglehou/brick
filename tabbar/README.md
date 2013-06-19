# Overview
Tab bars are used to display an app-level navigation/tabbing bar (usually at the bottom of the UI) that shows different content depending on which tab is selected.

# Usage

Basic usage (don't worry about the [shuffledeck](https://github.com/mozilla/app-components/tree/master/shuffledeck) structure, this is just for the demo): 

    <x-shuffledeck>
        <x-shuffleslide>One</x-shuffleslide>
        <x-shuffleslide>Two</x-shuffleslide>
    </x-shuffledeck>
    <x-tabbar>
        <x-tabbar-tab target-selector="x-shuffledeck x-shuffleslide:first-child">
            One
        </x-tabbar-tab>
        <x-tabbar-tab target-selector="x-shuffledeck x-shuffleslide:nth-child(2)">
            Two
        </x-tabbar-tab>
    </x-tabbar>
    
This will produce a tab bar whose tabs are linked to showing slides one and two, respectively. When the tabs are clicked, they will fire `show` events on their targeted elements.

Alternatively, if you don't want to have to work out the CSS selectors for each tab, you could assign the target dynamically using the `.targetElems` property instead of setting `target-selector` on each &lt;x-tabbar-tab&gt;:

    var slides = document.querySelectorAll('x-shuffleslide');
    var tabs = document.querySelectorAll('x-tabbar-tab');
    for(var i=0; i < slides.length && i < tabs.length; i++){
        tabs[i].targetElems = [slides[i]];
    }

# Attributes

## (x-tabbar-tab): ___target-selector___

Defines how to select the target elements of a particular tab. This can be any format that would be a valid CSS selector for document.querySelectorAll

# Accessors (getters/setters)

## ___tabs___ (getter only)

Returns a list of the &lt;x-tabbar-tab&gt; elements in the &lt;x-tabbar&gt;.

## (x-tabbar-tab): ___targetElems___ 

**getter**: Returns a list of the the elements targeted by the specific tab
**setter**: Assigns the tab's targeted elements as the given list of elements. (If targets are assigned using this dynamic assignment, the `target-selector` attribute is removed.)

# Events

## ___show___

Whenever a x-tabbar-tab is tapped/clicked, a `show` event is fired on each of its target elements. It is up to the target element to respond to this event. 

Components with default implemented responses to `show`:

* [Shuffledeck](https://github.com/mozilla/app-components/tree/master/shuffledeck) (`show` is applied to individual &lt;x-shuffleslide&gt;s)
* [Slidebox](https://github.com/x-tag/slidebox) (`show` is applied to individual &lt;x-slide&gt;s)
* [Flipbox](https://github.com/x-tag/flipbox) (`show` is applied to the front/back elements of the card)