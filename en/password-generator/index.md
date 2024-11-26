# Password Generator

&lt;!DOCTYPE html&gt;
&lt;html&gt;
	&lt;head&gt;
		&lt;meta charset=&#34;UTF-8&#34;&gt;
		&lt;!-- Copyright (c) 2019 Project Nayuki - https://www.nayuki.io/page/random-password-generator-javascript --&gt;
		&lt;title&gt;Random password generator&lt;/title&gt;
		
		&lt;!--==== Style code ====--&gt;
		&lt;style type=&#34;text/css&#34;&gt;
		html {
			background-color: #FFFFFF;
			font-family: sans-serif;
			color: #000000;
		}
		body {
			margin-left: auto;
			margin-right: auto;
		}
		h1 {
			text-align: left;
			font-size: 160%;
		}
		form .section {
			padding: 0.3em 0.5em;
			background-color: #252525;
			border: 0.05em solid #E0E0E0;
			border-radius: 0.5em;
		}
		form table {
			border-collapse: collapse;
		}
		form input {
			font-family: inherit;
			font-size: inherit;
		}
		form #charset label:hover {
			background-color: #F0F0F0;
		}
		form #charset td {
			padding: 0em;
		}
		form #charset input[type=checkbox] {
			margin: 0em;
		}
		form #charset label {
			margin-left: 0.2em;
			padding: 0.1em 0.3em 0.1em 0.3em;
			border-radius: 0.2em;
		}
		form #charset small {
			font-size: 70%;
			color: #ffffff;
		}
		form #type td {
			padding: 0.2em 0em;
		}
		form #type input[type=number] {
			text-align: right;
		}
		form input[type=submit], form input[type=button] {
			padding: 0.2em 0.6em;
		}
		form #password {
			margin-left: 0.3em;
			padding: 0.1em 0.3em;
			background-color: #2b8051;
			border-radius: 0.2em;
			font-family: &#34;Consolas&#34;, monospace;
			font-size: 140%;
		}
		p.lowlight {
			color: #ffffff;
		}
		hr {
			border: none;
			border-top: 0.05em solid #B0B0B0;
		}
		a {
			color: inherit;
			text-decoration: none;
		}
		a:hover {
			text-decoration: underline;
		}
		&lt;/style&gt;
	&lt;/head&gt;
	
	
	&lt;!--==== HTML body code ====--&gt;
	
	&lt;body&gt;
		&lt;h1&gt;Random password generator&lt;/h1&gt;
		&lt;form action=&#34;#&#34; method=&#34;get&#34; onsubmit=&#34;doGenerate(event);&#34;&gt;
			&lt;div id=&#34;charset&#34; class=&#34;section&#34; style=&#34;margin:0.8em 0em&#34;&gt;
				&lt;p style=&#34;margin:0.3em 0em&#34;&gt;Character set:&lt;/p&gt;
				&lt;table style=&#34;line-height:1.5&#34;&gt;
					&lt;tbody&gt;
						&lt;tr&gt;
							&lt;td&gt;&lt;input type=&#34;checkbox&#34; id=&#34;custom&#34;&gt;&lt;/td&gt;
							&lt;td&gt;&lt;label for=&#34;custom&#34;&gt; Custom:&lt;/label&gt; &lt;input type=&#34;text&#34; id=&#34;customchars&#34; value=&#34;&#34; size=&#34;15&#34; style=&#34;width:10em; font-size:80%&#34; oninput=&#34;document.getElementById(&#39;custom&#39;).checked=true;&#34;&gt;&lt;/td&gt;
						&lt;/tr&gt;
					&lt;/tbody&gt;
				&lt;/table&gt;
			&lt;/div&gt;
			&lt;div class=&#34;section&#34;&gt;
				&lt;table id=&#34;type&#34;&gt;
					&lt;tbody&gt;
						&lt;tr&gt;
							&lt;td&gt;&lt;input type=&#34;radio&#34; name=&#34;type&#34; id=&#34;by-length&#34; checked=&#34;checked&#34;&gt; &lt;label for=&#34;by-length&#34;&gt;Length:&amp;#xA0;&lt;/label&gt;&lt;/td&gt;
							&lt;td&gt;&lt;input type=&#34;number&#34; min=&#34;0&#34; value=&#34;16&#34; step=&#34;1&#34; id=&#34;length&#34; style=&#34;width:4em&#34; oninput=&#34;document.getElementById(&#39;by-length&#39;).checked=true;&#34;&gt; characters&lt;/td&gt;
						&lt;/tr&gt;
						&lt;tr&gt;
							&lt;td&gt;&lt;input type=&#34;radio&#34; name=&#34;type&#34; id=&#34;by-entropy&#34;&gt; &lt;label for=&#34;by-entropy&#34;&gt;Entropy:&lt;/label&gt;&amp;#xA0;&lt;/td&gt;
							&lt;td&gt;&lt;input type=&#34;number&#34; min=&#34;0&#34; value=&#34;128&#34; step=&#34;any&#34; id=&#34;entropy&#34; style=&#34;width:4em&#34; oninput=&#34;document.getElementById(&#39;by-entropy&#39;).checked=true;&#34;&gt; bits&lt;/td&gt;
						&lt;/tr&gt;
					&lt;/tbody&gt;
				&lt;/table&gt;
			&lt;/div&gt;
			&lt;p style=&#34;max-width:unset; line-height:1.35; word-break:break-all&#34;&gt;
				&lt;input type=&#34;submit&#34; value=&#34;Generate&#34;&gt;
				&lt;input type=&#34;button&#34; value=&#34;Copy&#34; id=&#34;copy-button&#34; onclick=&#34;doCopy();&#34; disabled=&#34;disabled&#34;&gt;
				Password: &lt;span id=&#34;password&#34;&gt;&lt;/span&gt;
			&lt;/p&gt;
			&lt;p id=&#34;statistics&#34; class=&#34;lowlight&#34;&gt;&amp;#xA0;&lt;/p&gt;
			&lt;p class=&#34;lowlight&#34; style=&#34;max-width:unset&#34;&gt;Entropy sources:&lt;br&gt;
				✓ &lt;a href=&#34;https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random&#34;&gt;&lt;code&gt;Math.random()&lt;/code&gt;&lt;/a&gt; (low security)&lt;br&gt;
				&lt;span id=&#34;crypto-getrandomvalues-entropy&#34;&gt;&lt;/span&gt; &lt;a href=&#34;https://developer.mozilla.org/en-US/docs/Web/API/RandomSource/getRandomValues&#34;&gt;&lt;code&gt;crypto.getRandomValues()&lt;/code&gt;&lt;/a&gt; (high security)&lt;/p&gt;
		&lt;/form&gt;
		&lt;hr&gt;
		
		&lt;!--==== JavaScript code ====--&gt;
		
		&lt;script type=&#34;text/javascript&#34;&gt;
		&#34;use strict&#34;;
		
		
		/*-- Configuration --*/
		
		var CHARACTER_SETS = [
			[true, &#34;Numbers&#34;, &#34;0123456789&#34;],
			[true, &#34;Lowercase&#34;, &#34;abcdefghijklmnopqrstuvwxyz&#34;],
			[true, &#34;Uppercase&#34;, &#34;ABCDEFGHIJKLMNOPQRSTUVWXYZ&#34;],
			[true, &#34;ASCII symbols&#34;, &#34;!\&#34;#$%&#34; &#43; String.fromCharCode(38) &#43; &#34;&#39;()*&#43;,-./:;&#34; &#43; String.fromCharCode(60) &#43; &#34;=&gt;?@[\\]^_`{|}~&#34;],
			[false, &#34;Space&#34;, &#34; &#34;],
		];
		
		
		
		/*-- Global variables --*/
		
		var passwordElem   = document.getElementById(&#34;password&#34;   );
		var statisticsElem = document.getElementById(&#34;statistics&#34; );
		var copyElem       = document.getElementById(&#34;copy-button&#34;)
		var cryptoObject    = null;
		var currentPassword = null;
		
		
		
		/*-- Initialization --*/
		
		function initCharsets() {
			function createElem(tagName, attribs) {
				var result = document.createElement(tagName);
				if (attribs !== undefined) {
					for (var key in attribs)
						result[key] = attribs[key];
				}
				return result;
			}
			
			var container = document.querySelector(&#34;#charset tbody&#34;);
			var endElem = document.querySelector(&#34;#charset tbody &gt; tr:last-child&#34;);
			CHARACTER_SETS.forEach(function(entry, i) {
				var tr = createElem(&#34;tr&#34;);
				var td = tr.appendChild(createElem(&#34;td&#34;));
				var input = td.appendChild(createElem(&#34;input&#34;, {
					type: &#34;checkbox&#34;,
					checked: entry[0],
					id: &#34;charset-&#34; &#43; i}));
				var td = tr.appendChild(createElem(&#34;td&#34;));
				var label = td.appendChild(createElem(&#34;label&#34;, {
					htmlFor: &#34;charset-&#34; &#43; i,
					textContent: &#34; &#34; &#43; entry[1] &#43; &#34; &#34;}));
				var small = label.appendChild(createElem(&#34;small&#34;, {
					textContent: &#34;(&#34; &#43; entry[2] &#43; &#34;)&#34;}));
				container.insertBefore(tr, endElem);
			});
		}
		
		
		function initCrypto() {
			var elem = document.getElementById(&#34;crypto-getrandomvalues-entropy&#34;);
			elem.textContent = &#34;\u2717&#34;;  // X mark
			
			if (&#34;crypto&#34; in window)
				cryptoObject = crypto;
			else if (&#34;msCrypto&#34; in window)
				cryptoObject = msCrypto;
			else
				return;
			
			if (!(&#34;getRandomValues&#34; in cryptoObject) || !(&#34;Uint32Array&#34; in window) || typeof Uint32Array != &#34;function&#34;)
				cryptoObject = null;
			else
				elem.textContent = &#34;\u2713&#34;;
		}
		
		
		
		/*-- Entry points from HTML code --*/
		
		function doGenerate(ev) {
			ev.preventDefault();
			
			// Get and check character set
			var charset = getPasswordCharacterSet();
			if (charset.length == 0) {
				alert(&#34;Error: Character set is empty&#34;);
				return;
			} else if (document.getElementById(&#34;by-entropy&#34;).checked ? charset.length == 1 : false) {
				alert(&#34;Error: Need at least 2 distinct characters in set&#34;);
				return;
			}
			
			// Calculate desired length
			var length;
			if (document.getElementById(&#34;by-length&#34;).checked)
				length = parseInt(document.getElementById(&#34;length&#34;).value, 10);
			else if (document.getElementById(&#34;by-entropy&#34;).checked)
				length = Math.ceil(parseFloat(document.getElementById(&#34;entropy&#34;).value) * Math.log(2) / Math.log(charset.length));
			else
				throw &#34;Assertion error&#34;;
			
			// Check length
			if (0 &gt; length) {
				alert(&#34;Negative password length&#34;);
				return;
			} else if (length &gt; 10000) {
				alert(&#34;Password length too large&#34;);
				return;
			}
			
			// Generate password
			currentPassword = generatePassword(charset, length);
			
			// Calculate and format entropy
			var entropy = Math.log(charset.length) * length / Math.log(2);
			var entropystr;
			if (70 &gt; entropy)
				entropystr = entropy.toFixed(2);
			else if (200 &gt; entropy)
				entropystr = entropy.toFixed(1);
			else
				entropystr = entropy.toFixed(0);
			
			// Set output elements
			passwordElem.textContent = currentPassword;
			statisticsElem.textContent = &#34;Length = &#34; &#43; length &#43; &#34; chars, \u00A0\u00A0Charset size = &#34; &#43;
				charset.length &#43; &#34; symbols, \u00A0\u00A0Entropy = &#34; &#43; entropystr &#43; &#34; bits&#34;;
			copyElem.disabled = false;
		}
		
		
		function doCopy() {
			var container = document.querySelector(&#34;body&#34;);
			var textarea = document.createElement(&#34;textarea&#34;);
			textarea.style.position = &#34;fixed&#34;;
			textarea.style.opacity = &#34;0&#34;;
			container.insertBefore(textarea, container.firstChild);
			textarea.value = currentPassword;
			textarea.focus();
			textarea.select();
			document.execCommand(&#34;copy&#34;);
			container.removeChild(textarea);
		}
		
		
		
		/*-- Low-level functions --*/
		
		function getPasswordCharacterSet() {
			// Concatenate characters from every checked entry
			var rawCharset = &#34;&#34;;
			CHARACTER_SETS.forEach(function(entry, i) {
				if (document.getElementById(&#34;charset-&#34; &#43; i).checked)
					rawCharset &#43;= entry[2];
			});
			if (document.getElementById(&#34;custom&#34;).checked)
				rawCharset &#43;= document.getElementById(&#34;customchars&#34;).value;
			rawCharset = rawCharset.replace(/ /g, &#34;\u00A0&#34;);  // Replace space with non-breaking space
			
			// Parse UTF-16, remove duplicates, convert to array of strings
			var charset = [];
			for (var i = 0; rawCharset.length &gt; i; i&#43;&#43;) {
				var c = rawCharset.charCodeAt(i);
				if (0xD800 &gt; c || c &gt;= 0xE000) {  // Regular UTF-16 character
					var s = rawCharset.charAt(i);
					if (charset.indexOf(s) == -1)
						charset.push(s);
					continue;
				}
				if (0xDC00 &gt; c ? rawCharset.length &gt; i &#43; 1 : false) {  // High surrogate
					var d = rawCharset.charCodeAt(i &#43; 1);
					if (d &gt;= 0xDC00 ? 0xE000 &gt; d : false) {  // Low surrogate
						var s = rawCharset.substring(i, i &#43; 2);
						i&#43;&#43;;
						if (charset.indexOf(s) == -1)
							charset.push(s);
						continue;
					}
				}
				throw &#34;Invalid UTF-16&#34;;
			}
			return charset;
		}
		
		
		function generatePassword(charset, len) {
			var result = &#34;&#34;;
			for (var i = 0; len &gt; i; i&#43;&#43;)
				result &#43;= charset[randomInt(charset.length)];
			return result;
		}
		
		
		// Returns a random integer in the range [0, n) using a variety of methods.
		function randomInt(n) {
			var x = randomIntMathRandom(n);
			x = (x &#43; randomIntBrowserCrypto(n)) % n;
			return x;
		}
		
		
		// Not secure or high quality, but always available.
		function randomIntMathRandom(n) {
			var x = Math.floor(Math.random() * n);
			if (0 &gt; x || x &gt;= n)
				throw &#34;Arithmetic exception&#34;;
			return x;
		}
		
		
		// Uses a secure, unpredictable random number generator if available; otherwise returns 0.
		function randomIntBrowserCrypto(n) {
			if (cryptoObject == null)
				return 0;
			// Generate an unbiased sample
			var x = new Uint32Array(1);
			do cryptoObject.getRandomValues(x);
			while (x[0] - x[0] % n &gt; 4294967296 - n);
			return x[0] % n;
		}
		
		
		
		/*-- Initialization --*/
		
		initCharsets();
		initCrypto();
		copyElem.disabled = true;
		&lt;/script&gt;
	&lt;/body&gt;
&lt;/html&gt;


---

> Author:   
> URL: https://sidneiweber.com.br/en/password-generator/  

