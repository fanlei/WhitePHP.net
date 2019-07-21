---
layout: post
title: "The Little PHPer - 6. Shadows"
---

<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP <span class="sc-ref">[<a href="https://github.com/whitephp/the-little-phper/blob/master/src/chapter_6.php" target="_whitephp-ref">Source Code</a>]</span>
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            <code>
            numbered?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_numbered
($aexp)
{return 
    is_atom($aexp) ? is_number($aexp)
    : (   is_eq(car(cdr($aexp)), '+')
       || is_eq(car(cdr($aexp)), 'x')
       || is_eq(car(cdr($aexp)), '^'))
      && is_numbered(car($aexp))
      && is_numbered(car(cdr(cdr($aexp))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            value
            </code>
            </td>
            <td>
            {%- highlight php -%}
function value
($nexp)
{return 
    is_atom($nexp) ? $nexp
    : (is_eq(car(cdr($nexp)), '+') ? 
      plus(value(car($nexp)),
           value(car(cdr(cdr($nexp)))))
      : (is_eq(car(cdr($nexp)), 'x') ? 
          x(value(car($nexp)),
            value(car(cdr(cdr($nexp)))))
        : power(value(car($nexp)),
                value(car(cdr(cdr($nexp)))))));
}
            {%- endhighlight -%}
            {%- highlight php -%}
function value
($nexp)
{return 
    is_atom($nexp) ? $nexp
    : (is_eq(operator($nexp), '+') ?
        plus(value(first_sub_exp($nexp)),
             value(second_sub_exp($nexp)))
      : (is_eq(operator($nexp), 'x') ?
          x(value(first_sub_exp($nexp)),
            value(second_sub_exp($nexp)))
        : power(value(first_sub_exp($nexp)),
                value(second_sub_exp($nexp)))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            2nd-sub-exp
            </code>
            </td>
            <td>
            {%- highlight php -%}
function second_sub_exp
($aexp)
{return
    car(cdr(cdr($aexp)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            1st-sub-exp
            </code>
            </td>
            <td>
            {%- highlight php -%}
// prefix
function first_sub_exp
($aexp)
{return 
    car(cdr($aexp));
}
            {%- endhighlight -%}
            {%- highlight php -%}
// infix
use function car as first_sub_exp;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            operator
            </code>
            </td>
            <td>
            {%- highlight php -%}
// prefix
use function car as operator;
            {%- endhighlight -%}
            {%- highlight php -%}
// infix
function operator
($nexp)
{return 
    car(cdr($nexp));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            sero?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_sero
($n)
{return
    is_nulll($n);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            edd1
            </code>
            </td>
            <td>
            {%- highlight php -%}
function edd1
($n)
{return 
    cons([], $n);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            zub1
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function cdr as zub1;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            blus
            </code>
            </td>
            <td>
            {%- highlight php -%}
function blus
($n, $m)
{return 
    is_sero($m) ? $n
    : edd1(blus($n, zub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
