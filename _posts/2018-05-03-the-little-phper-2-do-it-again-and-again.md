---
layout: post
title: "The Little PHPer - 2. Do It, Do It Again, and Again, and Again..."
---

<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <pre>
(define foo
  (lambda (a b c) 
    (body
    )))
                </pre>
            </td>
            <td>
                <pre>
function foo        |       $foo = function
($a, $b, $c)        |       ($a, $b, $c) use (&$foo)
{return             |       {return
    body;           |           body;
}                   |       };</pre>
                <div class="sup-block"><sup><a href="#php-function">[1]</a>,</sup> <sup><a href="#php-lambda">[2]</a></sup></div>
            </td>
        </tr>
        <tr>
            <td>
                <pre>
(cond 
  (p1 e1)
  (p2 e2)
  ...
  (else en))</pre>
            </td>
            <td>
            <br />
                <pre>
p1 ? e1 
: (p2 ? e2
  ...
  : en);</pre>
                <div class="sup-block"><sup><a href="#php-ternary">[3]</a></sup></div>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                    #t
                </code>
            </td>
            <td>
                <code>TRUE</code> <sup><a href="#php-boolean">[4]</a></sup>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                    #f
                </code>
            </td>
            <td>
                <code>
                    FALSE
                </code>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                (or ...)
                </code>
            </td>
            <td>
                <code>... or ...</code> 
                <sup><a href="#php-logical">[5]</a></sup>
            </td>
        </tr>
        <tr>
            <td>
                <pre>
(define lat?
  (lambda l
    (cond
      ((null? l) #t)
      ((atom? (car l)) (lat? (cdr l)))
      (else #f))))</pre>
            </td>
            <td>
            {%- highlight php -%}
function is_lat
($l)
{return 
    is_nulll($l) ? TRUE 
    : (is_atom(car($l)) ? is_lat(cdr($l))
      : FALSE);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
                <pre>
(define member?
  (lambda (a lat)
    (cond
      ((null? lat) #f)
      (else (or (eq? (car lat) a)
              (member? a (cdr lat)))))))</pre>
            </td>
            <td>
            {%- highlight php -%}
function is_member
($a, $lat)
{return 
    is_nulll($l) ? FALSE 
    : is_eq($a, car($lat)) || is_member($a, cdr($lat));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>

<ol>
    <li id="php-function"><a href="https://www.php.net/manual/en/functions.user-defined.php" target="_whitephp-ref">PHP User-defined functions</a>.</li>
    <li id="php-lambda"><a href="https://www.php.net/manual/en/functions.anonymous.php" target="_whitephp-ref">PHP Anonymous functions</a>.</li>
    <li id="php-ternary"><a href="https://www.php.net/manual/en/language.operators.comparison.php#language.operators.comparison.ternary" target="_whitephp-ref">PHP Ternary Operator</a>.</li>
    <li id="php-boolean"><a href="https://www.php.net/manual/en/language.types.boolean.php" target="_whitephp-ref">PHP Booleans</a>.</li>
    <li id="php-logical"><a href="https://www.php.net/manual/en/language.operators.logical.php" target="_whitephp-ref">PHP Logical</a>.</li>
<p></p>
</ol>

