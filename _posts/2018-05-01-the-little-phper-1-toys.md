---
layout: post
title: "The Little PHPer - 1. Toys"
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
                atom
            </td>
            <td>
                non-array <sup><a href="#php-types">[1]</a></sup>
            </td>
        </tr>
        <tr>
            <td>
                <code>atom</code><br />
                <code>(quote atom)</code>
            </td>
            <td>
                <code>'atom'</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>1492</code>
            </td>
            <td>
                <code>1492</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>*abc$</code>
            </td>
            <td>
                <code>'*abc$'</code>
            </td>
        </tr>
        <tr>
            <td>
                list <sup><a href="#s-expression">[2]</a></sup>
            </td>
            <td>
                array <sup><a href="#php-array">[3]</a></sup>
            </td>
        </tr>
        <tr>
            <td>
                <code>(atom)</code><br />
                <code>(quote (atom))</code>
            </td>
            <td>
                <code>['atom']</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>(atom turkey or)</code>
            </td>
            <td>
                <code>['atom', 'turkey', 'or']</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>((atom, turkey) or)</code>
            </td>
            <td>
                <code>[['atom', 'turkey'], 'or']</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>(((how) are) ((you) (doing so)) far)</code>
            </td>
            <td>
                <code>[[['how'], 'are'] [['you'], ['doing', 'so']], 'far']</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>()</code>
            </td>
            <td>
                <code>[]</code>
            </td>
        </tr>
        <tr>
            <td>
                <code>(() () ())</code>
            </td>
            <td>
                <code>[[], [], []]</code>
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>car</code>
            </td>
            <td>
            {%- highlight php -%}
function car
($l)
{return 
    $l[0];
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>cdr</code> <sup><a href="#car-and-cdr">[4]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function cdr
($l)
{return 
    array_slice($l, 1);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>cons</code>
            </td>
            <td>
            {%- highlight php -%}
function cons
($s, $l)
{return
    array_merge([$s], $l);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>null?</code>
            </td>
            <td>
            {%- highlight php -%}
function is_nulll
($l)
{return
    [] === $l;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>atom?</code>
            </td>
            <td>
            {%- highlight php -%}
function is_atom
($s)
{return
    ! is_array($s);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td class="primitive">
                <code>eq?</code>
            </td>
            <td>
            {%- highlight php -%}
function is_eq
($s1, $s2)
{return
    $s1 === $s2;
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>

<ol>
    <li id="php-types"><a href="https://php.net/manual/en/language.types.intro.php" target="_whitephp-ref">PHP Types</a>.</li>
    <li id="s-expression"><a href="https://en.wikipedia.org/wiki/S-expression" target="_whitephp-ref">S-expression</a>.</li>
    <li id="php-types"><a href="https://www.php.net/manual/en/language.types.array.php" target="_whitephp-ref">PHP Array</a>, <q>treated as an array</q>.</li>
    <li id="car-and-cdr">Why <a href="https://en.wikipedia.org/wiki/CAR_and_CDR" target="_whitephp-ref">Car and Cdr</a>?</li>
<p></p>
</ol>
