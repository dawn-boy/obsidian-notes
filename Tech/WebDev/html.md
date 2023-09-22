# Comments
```html
<!-- anything between this is a comment. -->
```
# tags
#### h 
```html
<h1>Hello</h1>
<h2>Hello</h2>
<h3>Hello</h3>
<h4>Hello</h4>
<h5>Hello</h5>
<h6>Hello</h6>
```
#### p 
```html
<p>Hello there's a Para here!</p>
```
#### img 
```html
<img src='https://somewhere' alt='some description for visually challenged people' />
```
#### list
```html
<!-- Ordered Lists -->
<ol>
	<li>something</li>
	<li>something</li>
	<li>something</li>
	<li>something</li>
</ol>

<!-- Unordered Lists -->
<ul>
	<li>something</li>
	<li>something</li>
	<li>something</li>
	<li>something</li>
</ul>
```
#### a 
```html
<a href='arriving somewhere but not here'>Be gone!</a>
```
#### div 
```html
<div>
<!-- anything can go here, div is just used to group elements. It's generic really, it's an block element, so you get your own cabin! -->
</div>
```
#### span 
```html
<span>
<!-- span is an inline element, it can be used to single out a content so we can style it differently latter. -->
</span>
```
#### hr
```html
<!-- prints a sep line. that's it. -->
<hr>
```
#### br
```html
<!-- it breaks and all the following text is printed in the next line. -->
<br>
```
#### sup and sub
```html
<!-- superscript -->
<sup>Get me up and it's all over.</sup>
<!-- subscript -->
<sub>Get me down and it's all over.</sub>
```
#### tables
```html
<table>
	<thead>
		<tr rowspan='2'>
			<th></th>
		</tr>
		<tr colspan='2'>
			<th></th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td></td>
		</tr>
	</tfoot>
</table>
```
#### forms
```html
<form action="/search/">
	<label for='name'>Name yourself!</label>
	<input name='name' type='text' id='name' placeholder='Type your Text here!'>

	<label for='password'>Enter thy password</label>
	<input name='pass' type='password' id='password' placeholder='Password here!'>

	<label for='email'>Enter de Email</label>
	<input name='mail' type='email' for='email' placeholder="Emails here!">

	<label for='color'>Choose a color</label>
	<input name='color' type='color' id='color'>

	<label for='number'>Enter them number</label>
	<input name='number' type='number' id='number' placeholder='Number here!'>

<!-- The ID attribute is used to bind an element to another element having the given id. -->
<!-- The Name attribute is used to label the data that's sent over to the desired location. -->

</form>
```
#### button
```html
<button></button>

<!-- if the button is inside a form, it submits to the path in the action parameter -->
<form action='google.com'>
	<button>HEllo THere!</button>
</form>
```
## Semantic Markup
```html
<!-- nothing new from what <div> offers other than the new names! -->
<nav>
<section>
<article>
<aside>
<summary>
<details>
<footer>
<!-- chosing this over <div> in suitable scenarios, can help a search engine to crawl your site easily and recommend it to the public. -->


<!-- also gives meaning to the whole damn life. -->
```
# Entity codes
```html
<!-- entity code for ampersand himself! -->
&amp; <!-- this is how an entity code should be mentioned -->
<!-- enitity code for greater than sign -->
&gt;
<!-- entity code for diamonds symbol -->
&diams;
<!-- etc, etc, etc -->
```
