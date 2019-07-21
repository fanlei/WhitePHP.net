---
layout: post
title: "The Little PHPer - 9. ... and Again, and Again, and Again, ..."
---

<style>
.post-title {
    font-size: 31px;   
}
</style>

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
            <code>
            looking 
            </code>
            </td>
            <td>
            {%- highlight php -%}
function looking
($s, $l)
{return
    keep_looking($s, pick(1, $l), $l);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>keep-looking</code>
            <sup><a href="#partial-function">[1]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function keep_looking
($s, $sorn, $l)
{return
    is_number($sorn) ? keep_looking($s, pick($sorn, $l), $l)
    : is_eq($sorn, $s);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>eternity</code>
            </td>
            <td>
            {%- highlight php -%}
function eternity
($x)
{return
    eternity($x);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            shift
            </code>
            </td>
            <td>
            {%- highlight php -%}
function shift
($pair)
{return
    build(first(first($pair)), 
          build(second(first($pair)), 
                second($pair)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            align
            </code>
            </td>
            <td>
            {%- highlight php -%}
function align
($pora)
{return
    is_atom($pora) ? $pora 
    : (is_pair(first($pora)) ? align(shift($pora))
      : build(first($pora), align(second($pora))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            length*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function length_star
($pora)
{return
    is_atom($pora) ? 1
    : plus(length_star(first($pora)), length_star(second($pora)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            weight*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function weight_star
($pora)
{return
    is_atom($pora) ? 1
    : plus(x(weight_star(first($pora)), 2), 
             weight_star(second($pora)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            shuffle
            </code>
            </td>
            <td>
            {%- highlight php -%}
function shuffle
($pora) 
{return
    is_atom($pora) ? $pora
    : (is_pair(first($pora)) ? shuffle(revpair($pora))
      : build(first($pora), shuffle(second($pora))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>C</code>
            <sup><a href="#lothar-c">[2]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function C
($n)
{return
    is_one($n) ? 1
    : (is_even($n) ? C(division($n, 2))
      : C(add1(x(3, $n))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>A</code>
            <sup><a href="#wilhelm-a">[3]</a>,</sup>
            <sup><a href="#alan-t">[4]</a>,</sup>
            <sup><a href="#kurt-g">[5]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function A
($n, $m)
{return
    is_zero($n) ? add1($m)
    : (is_zero($m) ? A(sub1($n), 1)
      : A(sub1($n), A($n, sub1($m))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>Y</code>
            <sup><a href="#y-combinator">[6]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function Y
($le)
{return
    (function ($f) 
     {return
        $f($f);
     })(function ($f) use ($le) 
        {return
            $le(function ($x) use ($f) 
                {return
                    $f($f)($x);
                });
        });
}
            {%- endhighlight -%}
            <sup><a href="#y-in-php">[7]</a></sup>
            </td>
        </tr>
    </tbody>
</table>

<ol>
    <li id="partial-function"><a href="https://en.wikipedia.org/wiki/Partial_function" target="_whitephp-ref">Partial function/Total function</a></li>
    <li id="lothar-c"><a href="https://en.wikipedia.org/wiki/Lothar_Collatz" target="_whitephp-ref">Lothar Collatz</a></li>
    <li id="wilhelm-a"><a href="https://en.wikipedia.org/wiki/Wilhelm_Ackermann" target="_whitephp-ref">Wilhelm Ackermann</a></li>
    <li id="kurt-g"><a href="https://en.wikipedia.org/wiki/Gödel%27s_incompleteness_theorems" target="_whitephp-ref">Kurt Gödel</a></li>
    <li id="alan-t"><a href="https://en.wikipedia.org/wiki/Halting_problem" target="_whitephp-ref">Alan Turing</a></li>
    <li id="y-combinator"><a href="https://en.wikipedia.org/wiki/Y_Combinator" target="_whitephp-ref">Y Combinator</a></li>
    <li id="y-in-php"><a href="https://php100.wordpress.com/2009/04/13/php-y-combinator/" target="_whitephp-ref">Y Combinator in PHP</a></li>
<p></p>
</ol>
