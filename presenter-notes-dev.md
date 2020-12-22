# Accessibility For Web Developers

## Intro

Hi everyone, thank you for joining my second presentation on accessibility. This presentation touches on topics that are related to development work, but I think it is also beneficial to non-developers. I will try to balance between the technical details and general accessibility knowledge. As always, feel free to ask questions or put your questions or comments in the chat at any time. 

## Topics

The topics I'm going to cover today include semantic HTML, keyboard and focus management, and ARIA. I will also share an accessibility checklist for developers and a few dev tools. These topics are related to some of most common accessibility issues that developers will need to address. I hope these could serve as starting points for you to learn other accessibility topics. 

## Semantics

The first topic is semantics, which means the correct interpretation of the meaning of a word, a sentence, or in our case, the code. A great deal of web content can be made accessible just by making sure the correct HTML elements are used for the correct purpose at all times. 

You might wonder why this is so important. After all, you could use div with CSS and JavaScript to make just about any web content. But semantic HTML does not take any longer to write than non-semantic HTML, if you do it consistently from the start. Even better, semantic HTML has benefits in accessibility and beyond.

## Why semantic HMTL

As you probably see in the example, semantic HTML is easier to read and understand. You don't have to look at the CSS class or ID to understand what an element is used for. 

Semantic HTML leads to more consistent code. For example, when we need a header, using non-semantic HTML, different developers may write the header as <div class="header">, <div id="header">, or simply <div>. There are so many ways that we can create a header element, and they all depend on the personal preferences of developers. Using a standard semantic HTML element makes it easier for everyone.

When we write semantic HTML, we’re letting the browser know what type of content it’s dealing with and how that content relates to other content. By doing this, assistive technology is more easily able to do its job because it has a structure that it can work with. Other technologies like the browser's reader mode, smart assistants like Siri and Alexa can also use information in the semantic HTML to display the correct content and styling. Search engines give more importance to keywords inside headings, links, etc. than keywords included in non-semantic <div>s, so content in semantic HTML will be more discoverable by users.

## Semantics in native HTML

Most HTML elements have implicit, or built-in semantics, mostly about their roles and states. These native HTML elements work reliably across browsers, so we should take advantage of their built-in accessibility support.

## Keyboard and focus management

Keyboard users should be able to access all functionalities without using the mouse. As mentioned in the first presentation, keyboard uers use the Tab and Shift + Tab keys to move forward and backward the focus to use the interactive content. 

## Why do we need ARIA

In our case, we need ARIA to create our own accessible widgets and elements that are not available as native HTML elements. 

For React, ARIA attributes are fully supported in JSX, and therefore can be used as attributes for elements and components. Unlike most attributes, ARIA attributes should be lowercased when declared, but the fundamental usage remains the same as in HTML.

## Accessibilty and React

Create a ref for the component you want to add focus on. Attach the created ref to the element. Set the focus with a lifecycle method.

Most React applications have routing. When a user navigates to a new page, nothing is announced by screen reader users. It's like nothing even happened. We can fix the React router problem with focus management. For example, when we change to a new page, we need to change the focus to the new component that was just mounted.