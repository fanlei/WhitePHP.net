---
layout: post
title: "The Little PHPer - 3. Cons the Magnificent"
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
            <code>
            rember
            </code>
            </td>
            <td>
            {%- highlight php -%}
function rember
($s, $l)
{return
    is_nulll($l) ? [] 
    : (is_eq(car($l), $s) ? cdr($l) 
      : cons(car($l), rember($s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            firsts
            </code>
            </td>
            <td>
            {%- highlight php -%}
function firsts
($l)
{return
    is_nulll($l) ? [] 
    : cons(car(car($l)), firsts(cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertR
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_right
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ? cons($old_s, cons($new_s, cdr($l)))
      : cons(car($l), insert_right($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertL
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_left
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ? cons($new_s, $l)
      : cons(car($l), insert_left($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            subst
            </code>
            </td>
            <td>
            {%- highlight php -%}
function subst
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ? cons($new_s, cdr($l))
      : cons(car($l), subst($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            subst2
            </code>
            </td>
            <td>
            {%- highlight php -%}
function subst2
($new_s, $old_s1, $old_s2, $l)
{return 
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s1) || is_eq(car($l), $old_s2) ? 
        cons($new_s, cdr($l))
      : cons(car($l), subst2($new_s, $old_s1, $old_s2, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multirember
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multirember
($s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $s) ? multirember($s, cdr($l))
      : cons(car($l), multirember($s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multiinsertR
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multiinsert_right
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ? 
        cons($old_s, 
             cons($new_s, 
                    multiinsert_right($new_s, $old_s, cdr($l))))
      : cons(car($l), multiinsert_right($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multiinsertL
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multiinsert_left
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ?
            cons($new_s,
                 cons($old_s,
                    multiinsert_left($new_s, $old_s, cdr($l))))
      : cons(car($l), multiinsert_left($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multisubst
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multisubst
($new_s, $old_s, $l)
{return
    is_nulll($l) ? []
    : (is_eq(car($l), $old_s) ?
       cons($new_s, multisubst($new_s, $old_s, cdr($l)))
      : cons(car($l), multisubst($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
