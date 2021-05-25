# Markdown provides backslash escapes for the following characters:

\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark

# Header
<h1> ===========
<h2> -----------
<h3> ### (1-6 hash marks)


<blockquote><p>This is a blockquote.</p></blockquote> 
> This is a blockquote.


<em>are emphasized</em> 
*are emphasized*
_are emphasized also_


<strong>strong emphasis</strong>
**strong emphasis**
__two underscores strong emphasis also__


<ul><li>Candy.</li></ul>
*   Candy.
+   Candy.
-   Candy.
use asterisks, pluses, and hyphens (*, +, and -) as list markers


<ol>
  <li>Red</li>
  <li>Green</li>
</ol>
1.  Red
2.  Green


<p>Example link <a href="http://google.com/" title="Google">Google</a> and <a href="http://www.nytimes.com/">The New York Times</a>.</p>
Example name link [Google][1] and [The New York Times][NY Times].

[1]: http://google.com/        "Google"
[ny times]: http://www.nytimes.com/


<img src="/path/to/img.jpg" alt="alt text" title="Title" />
![alt text](/path/to/img.jpg "Title")
Inline (titles are optional) or Reference-style:
![alt text][id]

[id]: /path/to/img.jpg "Title"


<p>Example code <code>&lt;blink&gt;</code> tags or <code>&amp;mdash;</code>.</p>
Example code `<blink>` tags or `&mdash;`.


<p>This is a normal paragraph:</p>
<pre><code>This is a code block by at least 4 spaces or 1 tab.</code></pre>
This is a normal paragraph:
    This is a code block by at least 4 spaces or 1 tab.


<p>A single backtick in a code span: <code>`</code></p>

A single backtick in a code span: `` ` ``

<p>A backtick-delimited string in a code span: <code>`foo`</code></p>

A backtick-delimited string in a code span: `` `foo` ``