<h1>PHP Coding Standards</h1>

Always use <code><?php</code> to delimit PHP code. Do not use the shorthand version, <code><?</code>. PHP short tags are not enabled by default on new installations and are deprecated.

<h2>Use PHP 5 Conventions</h2>
<ul>
  <li>Class constructors should use <code>public function __construct() {}</code> rather than the PHP 4 style class name.</li>
  <li>Use class destructors where appropriate.</li>
  <li>Explicitly declare visibility of member methods and variables (public, private, protected).</li>
  <li>
    Do <strong>NOT</strong> use closing tags for files containing only PHP code.
    <blockquote>
      The <code>?></code> at the end of code files is purposely omitted. This includes for module and include files. ... Removing it eliminates the possibility for unwanted whitespace at the end of files which can cause "header already sent" errors, XHTML/XML validation issues, and other problems.
    </blockquote>
  </li>
</ul>

<h2>Indenting and Whitespace</h2>
<ul>
  <li>Use indent of 2 spaces, no tabs.</li>
  <li>Leave no trailing whitespace at the end of lines.</li>
  <li>Files should be formatted with Unix line endings.</li>
</ul>

<h2>Operators</h2>
<ul>
  <li>Binary operators (<code>+, =, !=, -, ==, >,</code> etc.) should include a space before and after the operator, for readability. For instance, an assignment would be formatted as <code>$lorem = $ipsum</code> rather than <code>$lorem=$ipsum</code>.</li>
  <li>Unary operators (<code>++, --</code>) should not have a space between the operator and the variable or number they are operating on.</li>
</ul>

<h2>Casting</h2>
<p>Put a space between the (type) and the $variable in a cast: <code>(int) $mynumber</code>.</p>

<h2>Control Structures</h2>
<ul>
  <li>Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls.</li>
  <li>Always use curly braces even in situations where they are technically optional.</li>
  <li>Wrap ternary logic in parens.</li>
  <li>Don't use <code>else if</code>, but rather <code>elseif</code>.</li>
</ul>
<h3>Examples</h3>
<h5>If statements</h5>
<pre>
if (condition1 || condition2) {
  action1;
} elseif (condition3 && condition4) {
  action2;
} else {
  defaultaction;
}
</pre>
<h5>Switch statements</h5>
<pre>
switch (condition) {
  case 1:
    action1;
    break;

  case 2:
    action2;
    break;

  default:
    defaultaction;
}
</pre>
<h5>For statements</h5>
<pre>
for ($i = 0; $i &lt; condition; $i++) {
  action1;
}
</pre>

<h2>Control Structures in Templates</h2>
<ul>
  <li>In templates, a <code>:</code> may be used in place of brackets.</li>
  <li>Do no use a space between the closing paren and the colon.</li>
  <li>HTML inside the control structure should be indented.</li>
</ul>
Example:
<pre>
&lt;?php if (!empty($item)): ?&gt;
  &lt;p&gt;&lt;?php print $item; ?&gt;&lt;/p&gt;
&lt;?php endif; ?&gt;

&lt;?php foreach ($items as $item): ?&gt;
  &lt;p&gt;&lt;?php print $item; ?&gt;&lt;/p&gt;
&lt;?php endforeach; ?&gt;
</pre>

<h2>Function Calls</h2>
<ul>
  <li>Functions should be called with no spaces between the function name and the opening parenthesis.</li>
  <li>No space between the opening paren and the first parameter.</li>
  <li>Spaces between commas and each parameter.</li>
  <li>No space between the last parameter, the closing parenthesis, and the semicolon</li>
  <li>
    Here's an example:
    <code>$var = foo($bar, $apple, $peach);</code>
  </li>
</ul>

<h2>Arrays</h2>
<ul>
  <li>A space should separate each element.</li>
  <li>Add spaces around the => key association operator.</li>
  <li>Example: <code>$arr = array('hey', 'jude', 'git' => 'commit');</code></li>
  <li>If the array spans more than 80 characters, each element should be broken up on its own line.</li>
  <li>Multi-line declarations should have elements indented.</li>
</ul>
Example:
<pre>
$arr = array(
  'one' => $one,
  'two' => $two,
  'three' => $three,
  'four' => $four,
  'count' => 26
);
</pre>



<p>...more to come.</p>


<h2>Emacs Notes</h2>

Since the style guide is similar to Drupal's, we can steal some configuration from <a href="http://drupal.org/node/59868">this "drupal-mode</a>" for our php-mode (this goes in .emacs, naturally):

<pre>
(add-hook 'php-mode-hook
          (lambda ()
            (setq c-basic-offset 2)
            (setq indent-tabs-mode nil)
            (setq fill-column 78)
            (setq show-trailing-whitespace t)
            (add-hook 'before-save-hook 'delete-trailing-whitespace)
            (c-set-offset 'case-label '+)
            (c-set-offset 'arglist-close 0)
            (c-set-offset 'arglist-intro '+) ; for FAPI arrays and DBTNG
            (c-set-offset 'arglist-cont-nonempty 'c-lineup-math))) ; for DBTNG fields and values

</pre>