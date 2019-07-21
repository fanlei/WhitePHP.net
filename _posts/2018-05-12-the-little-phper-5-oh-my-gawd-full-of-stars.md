---
layout: post
title: "The Little PHPer - 5. *Oh My Gawd*:    It's Full of Stars"
---

<style>
.post-title {
    font-size: 35px;   
}
</style>

<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP <span class="sc-ref">[<a href="https://github.com/whitephp/the-little-phper/blob/master/src/chapter_5.php" target="_whitephp-ref">Source Code</a>]</span>
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            <code>
            rember*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function rember_star
($a, $l)
{return
    is_nulll($l) ? []
    : (is_atom(car($l)) ? 
        is_eq(car($l), $a) ? rember_star($a, cdr($l)) 
        : cons(car($l), rember_star($a, cdr($l)))
      : cons(rember_star($a, car($l)), rember_star($a, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertR*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_right_star
($new_s, $old_s, $l)
{return 
    is_nulll($l) ? []
    : (is_atom(car($l)) ? 
        is_eq(car($l), $old_s) ? 
          cons($old_s, cons($new_s, insert_right_star($new_s, $old_s, cdr($l)))) 
        : cons(car($l), insert_right_star($new_s, $old_s, cdr($l)))
      : cons(insert_right_star($new_s, $old_s, car($l)),
             insert_right_star($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            occur*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function occur_star
($a, $l)
{return
is_nulll($l) ? 0 
: (is_atom(car($l)) ?
    is_eq(car($l), $a) ? add1(occur_star($a, cdr($l)))
    : occur_star($a, cdr($l))
  : plus(occur_star($a, car($l)), occur_star($a, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            subst*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function subst_star
($new_s, $old_s, $l)
{return 
    is_nulll($l) ? []
    : (is_atom(car($l)) ?
        is_eq(car($l), $old_s) ? 
          cons($new_s, subst_star($new_s, $old_s, cdr($l)))
        : cons(car($l), subst_star($new_s, $old_s, cdr($l))) 
    : cons(subst_star($new_s, $old_s, car($l)),
           subst_star($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertL*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_left_star
($new_s, $old_s, $l)
{return 
    is_nulll($l) ? []
    : (is_atom(car($l)) ?
        is_eq(car($l), $old_s) ? 
          cons($new_s, cons($old_s, insert_left_star($new_s, $old_s, cdr($l))))
        : cons(car($l), insert_left_star($new_s, $old_s, cdr($l)))
      : cons(insert_left_star($new_s, $old_s, car($l)),
             insert_left_star($new_s, $old_s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            member*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function member_star
($a, $l)
{return
    is_nulll($l) ? FALSE
    : (is_atom(car($l)) ? is_eq(car($l), $a) || member_star($a, cdr($l))
      : member_star($a, car($l)) || member_star($a, cdr($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            leftmost
            </code>
            </td>
            <td>
            {%- highlight php -%}
function leftmost
($l)
{return 
    is_nulll($l) ? NULL 
    : (is_atom(car($l)) ? car($l) 
      : leftmost(car($l)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            equal?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_equal
($s1, $s2)
{return 
is_atom($s1) && is_atom($s2) ? is_eqan($s1, $s2)
: (is_atom($s1) || is_atom($s2) ? FALSE
   : is_eqlist($s1, $s2));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            eqlist?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_eqlist
($l1, $l2)
{return 
    is_nulll($l1) && is_nulll($l2) ? TRUE
    : (is_nulll($l1) || is_nulll($l2) ? FALSE
      : is_equal(car($l1), car($l2)) && is_eqlist(cdr($l1), cdr($l2)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            rember2
            </code>
            </td>
            <td>
            {%- highlight php -%}
function rember2
($s, $l)
{return
    is_nulll($l) ? []
    : (is_equal(car($l), $s) ? cdr($l)
      : cons(car($l), rember2($s, cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
