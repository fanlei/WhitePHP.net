---
layout: post
title: "The Little PHPer - 7. Friends and Relations"
---

<ul>
<li>
<i>pair</i>: consider only nonnegative integers.
</li>
<li>
<i>rel</i>: a list of numbers, could be empty.
</li>
<li>
<i>finite function</i>: a list of numbers, could be empty.
</li>
</ul>

<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP <span class="sc-ref">[<a href="https://github.com/whitephp/the-little-phper/blob/master/src/chapter_7.php" target="_whitephp-ref">Source Code</a>]</span>
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            <code>
            set?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_set
($l)
{return
    is_nulll($l) ? TRUE
    : (is_member(car($l), cdr($l)) ? FALSE
      : is_set(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            makeset
            </code>
            </td>
            <td>
            {%- highlight php -%}
function makeset
($l)
{return
    is_nulll($l) ? []
    : (is_member(car($l), cdr($l)) ? makeset(cdr($l))
      : cons(car($l), makeset(cdr($l))));
}
            {%- endhighlight -%}
            {%- highlight php -%}
function makeset
($l)
{return 
    is_nulll($l) ? []
    : cons(car($l), makeset(multirember(car($l), cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            subset?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_subset
($set1, $set2)
{return 
    is_nulll($set1) ? TRUE
    : is_member(car($set1), $set2) && is_subset(cdr($set1), $set2);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            eqset?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_eqset
($set1, $set2)
{return 
    is_subset($set1, $set2) && is_subset($set2, $set1);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            intersect?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_intersect
($set1, $set2)
{return 
    is_nulll($set1) ? FALSE
    : is_member(car($set1), $set2) || is_intersect(cdr($set1), $set2);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            intersect
            </code>
            </td>
            <td>
            {%- highlight php -%}
function intersect
($set1, $set2)
{return 
    is_nulll($set1) ? $set1
    : (is_member(car($set1), $set2) ? 
        cons(car($set1), intersect(cdr($set1), $set2))
      : intersect(cdr($set1), $set2));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            union
            </code>
            </td>
            <td>
            {%- highlight php -%}
function union
($set1, $set2)
{return 
    is_nulll($set1) ? $set2
    : (is_member(car($set1), $set2) ? union(cdr($set1), $set2)
      : cons(car($set1), union(cdr($set1), $set2)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            difference
            </code>
            </td>
            <td>
            {%- highlight php -%}
function difference
($set1, $set2)
{return 
    is_nulll($set1) ? []
    : (is_member(car($set1), $set2) ? difference(cdr($set1), $set2) 
      : cons(car($set1), difference(cdr($set1), $set2)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            intersectall
            </code>
            </td>
            <td>
            {%- highlight php -%}
function intersectall
($l_set)
{return
    is_nulll(cdr($l_set)) ? car($l_set)
    : intersect(car($l_set), intersectall(cdr($l_set)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            a-pair?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_pair
($x)
{return 
    is_atom($x) ? FALSE 
    : (is_nulll($x) ? FALSE
      : (is_nulll(cdr($x)) ? FALSE 
        : (is_nulll(cdr(cdr($x))) ? TRUE
          : FALSE)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            first
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function car as first;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            second
            </code>
            </td>
            <td>
            {%- highlight php -%}
function second
($l)
{return 
    car(cdr($l));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            build
            </code>
            </td>
            <td>
            {%- highlight php -%}
function build
($s1, $s2)
{return 
    cons($s1, cons($s2, []));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            third
            </code>
            </td>
            <td>
            {%- highlight php -%}
function third
($l)
{return
    car(cdr(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            fun?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_fun
($rel)
{return
    is_set(firsts($rel));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            revpair
            </code>
            </td>
            <td>
            {%- highlight php -%}
function revpair
($pair)
{return
    build(second($pair), first($pair));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            revrel
            </code>
            </td>
            <td>
            {%- highlight php -%}
function revrel
($rel)
{return 
    is_nulll($rel) ? $rel
    : cons(revpair(car($rel)), revrel(cdr($rel)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            seconds
            </code>
            </td>
            <td>
            {%- highlight php -%}
function seconds
($l)
{return 
    is_nulll($l) ? []
    : cons(second(car($l)), seconds(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            fullfun?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_fullfun
($fun)
{return 
    is_set(seconds($fun));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            one2one?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_one2one
($fun)
{return
    is_fun(revrel($fun));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
