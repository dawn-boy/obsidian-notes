# Comments
```html
<!-- anything between this is a comment. -->
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
	<!-- input for name -->
	<label for='name'>Name yourself!</label>
	<input name='usrName' type='text' id='name' placeholder='Type your Text here!'>

	<!-- input for password -->
	<label for='password'>Enter thy password</label>
	<input name='pass' type='password' id='password' placeholder='Password here!'>

	<!-- input for mail -->
	<label for='email'>Enter de Email</label>
	<input name='mail' type='email' for='email' placeholder="Emails here!">

	<!-- input for colro-->
	<label for='color'>Choose a color</label>
	<input name='usrColor' type='color' id='color'>
	
	<!-- input for number-->
	<label for='number'>Enter them number</label>
	<input name='phoneNumber' type='number' id='number' placeholder='Number here!'>

	<!-- input for checkboxes -->
	<label for='checkbox'>Like Jurassic Park?</label>
	<input name='decision' id='checkbox' type='checkbox'>

	<!-- input for radiabuttons -->
	<label for="radiobutton1">Part 1</label>
	<input name='radiobutton1' id='part' type='radio' />
	<label for="radiobutton2">Part 2</label>
	<input name='radiobutton2' id='part' type='radio' />
	<label for="radiobutton3">Part 3</label>
	<input name='radiobutton3' id='part' type='radio' />

	<!-- input for a selection of values -->
	<label for='selection'>Which Franchise</label>
	<select id='selection'>
		<option value='park'>Jurassic Park</option>
		<option value='world'>Jurassic World</option>
	</select>

	<!-- input for a larger text area -->
	<label for='textar'>Enter your comments</label>
	<textarea id='textar' rows=10></textarea>


<!-- The ID attribute is used to bind the input to it's label -->
<!-- The Name attribute is used to give a name to the data that's sent over to the action url-->
<!-- if there are mulitple radio buttons inside a form, only one of the can be selected at a time. -->

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

