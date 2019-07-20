---
layout: post
title: "The Little PHPer - 4. Numbers Games"
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
            <code><strong>
            add1
            </strong></code>
            </td>
            <td>
            {%- highlight php -%}
function add1
($n)
{return 
    $n + 1;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code><strong>
            sub1
            </strong></code>
            </td>
            <td>
            {%- highlight php -%}
function sub1
($n)
{return 
    $n - 1;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code><strong>
            zero?
            </strong></code>
            </td>
            <td>
            {%- highlight php -%}
function is_zero
($n)
{return 
    0 === $n;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &plus;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function plus
($n, $m)
{return
    is_zero($m) ? $n
    : add1(plus($n, sub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &minus;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function minus
($n, $m)
{return
    is_zero($m) ? $n
    : sub1(minus($n, sub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            addtup
            </code>
            </td>
            <td>
            {%- highlight php -%}
function addtup
($tup)
{return
    is_nulll($tup) ? 0
    : plus(car($tup), addtup(cdr($tup)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &times;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function x
($n, $m)
{return
    is_zero($m) ? 0
    : plus($n, x($n, sub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            tup&plus;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function tupplus
($tup1, $tup2)
{return 
    is_nulll($tup1) ? $tup2
    : (is_nulll($tup2) ? $tup1
      : cons(plus(car($tup1), car($tup2)), 
             tupplus(cdr($tup1), cdr($tup2))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &gt;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function gt
($n, $m)
{return
    is_zero($n) ? FALSE
    : is_zero($m) || gt(sub1($n), sub1($m));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &lt; 
            </code>
            </td>
            <td>
            {%- highlight php -%}
function lt
($n, $m)
{return
    is_zero($m) ? FALSE
    : is_zero($n) || lt(sub1($n), sub1($m));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &equals;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_eqn
($n, $m)
{return
    is_zero($n) ? is_zero($m)
    : (is_zero($m) ? FALSE
      : is_eqn(sub1($n), sub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &uarr;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function power
($n, $m)
{return
    is_zero($m) ? 1
    : x($n, power($n, sub1($m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            &div;
            </code>
            </td>
            <td>
            {%- highlight php -%}
function division
($n, $m)
{return
    is_zero($m) ? PHP_INT_MAX
    : (lt($n, $m) ? 0
      : add1(division(minus($n, $m), $m)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            length
            </code>
            </td>
            <td>
            {%- highlight php -%}
function length
($l)
{return
    is_nulll($l) ? 0
    : add1(length(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            pick
            </code>
            </td>
            <td>
            {%- highlight php -%}
function pick
($n, $l)
{return
    is_zero($n) ? NULL
    : (is_one($n) ? car($l)
      : pick(sub1($n), cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            rempick
            </code>
            </td>
            <td>
            {%- highlight php -%}
function rempick
($n, $l)
{return
    is_zero($n) ? $l
    : (is_nulll($l) ? []
      : (is_one($n) ? cdr($l)
        : cons(car($l), rempick(sub1($n), cdr($l)))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code><strong>
            number?
            </strong></code>
            </td>
            <td>
            {%- highlight php -%}
function is_number
($n)
{return
    is_int($n) && $n >=0;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            no-nums
            </code>
            </td>
            <td>
            {%- highlight php -%}
function no_nums
($l)
{return
    is_nulll($l) ? []
    : (is_number(car($l)) ? no_nums(cdr($l))
      : cons(car($l), no_nums(cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            all-nums
            </code>
            </td>
            <td>
            {%- highlight php -%}
function all_nums
($l)
{return
    is_nulll($l) ? []
    : (is_number(car($l)) ? cons(car($l), all_nums(cdr($l)))
      : all_nums(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            eqan?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_eqan
($a1, $a2)
{return 
    is_number($a1) && is_number($a2) ? is_eqn($a1, $a2)
    : (is_number($a1) || is_number($a1) ? FALSE
      : is_eq($a1, $a2));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            occur
            </code>
            </td>
            <td>
            {%- highlight php -%}
function occur
($a, $l)
{return
    is_nulll($l) ? 0
    : (is_eqan(car($l), $a) ? add1(occur($a, cdr($l)))
      : occur($a, cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            one?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_one
($n)
{return
    is_eqn($n, 1);
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
