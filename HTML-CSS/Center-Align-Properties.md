# Align-Properties

## Problem!
<img style="width:300px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FNWd59%2FbtrGHmUYzZM%2FEpExo9D62NTqdZk7Kc5Ft1%2Fimg.png" alt="img">

If you look at the logo in the picture above, there is a small gap between the parent element and the child element. 

I wanted to get rid of it because it bothered me to look at it, or I wanted to make the child elements vertically aligned and come to the center.<br/><br/><br/>


```html
<header class="logo"><img src="./img/logo.png" alt="logo"></header>
```
```css
.logo{
  width: 14rem;
  margin: 1.5em auto;
}
.logo img{
  width: 100%;
}
```
<br/>

### text-align?
A property used to horizontally align text elements. The image in the header above is not text, so it cannot be used in this situation.<br/><br/>

### align-items?
It is a vertical alignment property used for child elements in the flex state, so it cannot be used in this situation.<br/><br/>

### justify-content?
It is a horizontal alignment property that is used for parent elements when in a flex state, so it cannot be used in this situation.<br/><br/>

### margin: 0 auto?
It is an attribute value that can be used to horizontally align non-flex elements. The upper and lower margins are not given, and the left and right margins are automatically calculated by the computer and aligned in the middle. This property is not suitable for use in text elements because of its variability, so let's use the text-align property for text elements.
- Conditions!
1. 'Width' should be specified.
2. It is possible in block element. In the inline element, margin : 0 auto is not possible.<br/><br/>

### vertical align:middle?
It is a vertical alignment attribute used in inline and block. At this time, the height of the parent element must be specified. Padding or margin is also possible without giving exact height. The position of the vertical alignment may vary depending on the height value of the parent element.<br/><br/>

## Solution!
For this problem, the problem could be solved using vertical-align:middle.

<img style="width:200px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVdfS0%2FbtrGCCLZD4S%2FuEvOnOrimtmtuTrFwhUXvK%2Fimg.png" alt="img">

I should commit again when I get new information about align.👋