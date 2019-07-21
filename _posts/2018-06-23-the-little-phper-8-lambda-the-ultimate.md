---
layout: post
title: "The Little PHPer - 8. Lambda the Ultimate"
---

<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP <span class="sc-ref">[<a href="https://github.com/whitephp/the-little-phper/blob/master/src/chapter_8.php" target="_whitephp-ref">Source Code</a>]</span>
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            <code>
            rember-f
            </code>
            </td>
            <td>
            {%- highlight php -%}
function rember_f
($test, $s, $l)
{return 
    is_nulll($l) ? []
    : ($test(car($l), $s) ? cdr($l)
    : cons(car($l), rember_f($test, $s, cdr($l))));
}
            {%- endhighlight -%}
            {%- highlight php -%}
function rember_f
($test)
{return 
    function ($s, $l) use ($test) {
    return
        is_nulll($l) ? []
        : ($test(car($l), $s) ? cdr($l) 
          : cons(car($l), rember_f($test)($s, cdr($l))));
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>eq?-c</code> 
            <sup><a href="#currying">[1]</a>,</sup>
            <sup><a href="#moses-s">[2]</a>,</sup>
            <sup><a href="#haskell-c">[3]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function is_eq_c
($a)
{return 
    function ($x) use ($a)
    {return
        is_eq($x, $a);
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            eq?-salad
            </code>
            </td>
            <td>
            {%- highlight php -%}
$is_eq_salad = is_eq_c('salad');
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            rember-eq?
            </code>
            </td>
            <td>
            {%- highlight php -%}
$rember_is_eq = rember_f('is_eq');
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertL-f
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_left_f
($test)
{return
    function ($new_s, $old_s, $l) use ($test)
    {return 
        is_nulll($l) ? []
        : ($test(car($l), $old_s) ? cons($new_s, cons($old_s, cdr($l)))
          : cons(car($l), insert_left_f($test)($new_s, $old_s, cdr($l))));
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insertR-f
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_right_f
($test)
{return 
    function($new_s, $old_s, $l) use ($test)
    {return
    is_nulll($l) ? []
    : ($test(car($l), $old_s) ? cons($old_s, cons($new_s, cdr($l)))
      : cons(car($l), insert_right_f($test)($new_s, $old_s, cdr($l))));
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            seqL
            </code>
            </td>
            <td>
            {%- highlight php -%}
function seq_l
($new_s, $old_s, $l)
{return 
    cons($new_s, cons($old_s, $l));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            seq_r
            </code>
            </td>
            <td>
            {%- highlight php -%}
function seq_r
($new_s, $old_s, $l)
{return 
    cons($old_s, cons($new_s, $l));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            seqS
            </code>
            </td>
            <td>
            {%- highlight php -%}
function seq_s
($new_s, $old_s, $l)
{return 
    cons($new_s, $l);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            seqrem
            </code>
            </td>
            <td>
            {%- highlight php -%}
function seqrem
($new_s, $old_s, $l)
{return
    $l;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            insert-g
            </code>
            </td>
            <td>
            {%- highlight php -%}
function insert_g
($seq)
{return 
    function($new_s, $old_s, $l) use ($seq)
    {return 
        is_nulll($l) ? []
        : (is_eq(car($l), $old_s) ? $seq($new_s, $old_s, cdr($l)) 
          : cons(car($l), insert_g($seq)($new_s, $old_s, cdr($l))));
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            atom-to-function
            </code>
            </td>
            <td>
            {%- highlight php -%}
function atom_to_function
($operator)
{return
    is_eq($operator, '+') ? 'plus'
    : (is_eq($operator, 'x') ? 'x'
      : 'power');
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
    : atom_to_function(operator($nexp))
        (value(first_sub_exp($nexp)),
            value(second_sub_exp($nexp)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multirember-f
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multirember_f
($test)
{return 
    function($s, $l) use ($test)
    {return 
        is_nulll($l) ? []
        : ($test($s, car($l)) ? multirember_f($test)($s, cdr($l))
          : cons(car($l), multirember_f($test)($s, cdr($l))));
    };
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multirember-eq?
            </code>
            </td>
            <td>
            {%- highlight php -%}
$multirember_is_eq = multirember_f('is_eq');
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            eq?-tuna
            </code>
            </td>
            <td>
            {%- highlight php -%}
$is_eq_tuna = is_eq_c('tuna');
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>multirember&co</code>
            <sup><a href="#collector">[4]</a></sup>
            </td>
            <td>
            {%- highlight php -%}
function multirember_co
($s, $l, $col)
{return 
    is_nulll($l) ? $col([], [])
    : (is_eq($s, car($l)) ? 
      multirember_co($s, cdr($l),
          function ($new_l, $seen) use ($col, $l)
          {return // new-friend
              $col($new_l, cons(car($l), $seen));
          })
      : (multirember_co($s, cdr($l),
          function ($new_l, $seen) use ($col, $l)
          {return // latest-friend
              $col(cons(car($l), $new_l), $seen);
          })));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            a-friend
            </code>
            </td>
            <td>
            {%- highlight php -%}
function a_friend
($s_1, $s_2)
{return 
    is_nulll($s_2);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            last-friend
            </code>
            </td>
            <td>
            {%- highlight php -%}
function last_friend
($new_l, $seen)
{return 
    length($new_l);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multiinsertLR
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multiinsert_left_right
($new_s, $old_L, $old_R, $l)
{return
    is_nulll($l) ? []
    : (is_eq($old_L, car($l)) ?
      cons($new_s, cons($old_L,
            multiinsert_left_right($new_s, $old_L, $old_R, cdr($l))))
      : (is_eq($old_R, car($l)) ?
        cons($old_R, cons($new_s,
            multiinsert_left_right($new_s, $old_L, $old_R, cdr($l))))
        : (cons(car($l),
            multiinsert_left_right($new_s, $old_L, $old_R, cdr($l))))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            multiinsertLR&co
            </code>
            </td>
            <td>
            {%- highlight php -%}
function multiinsert_left_right_co
($new_s, $old_L, $old_R, $l, $col)
{return 
    is_nulll($l) ? $col([], 0, 0)
    : (is_eq($old_L, car($l)) ?
      multiinsert_left_right_co($new_s, $old_L, $old_R, cdr($l),
            function ($new_l, $n_L, $n_R) use ($col, $new_s, $old_L)
            {return
                $col(cons($new_s, cons($old_L, $new_l)), add1($n_L), $n_R);
            })
      : (is_eq($old_R, car($l)) ?
        multiinsert_left_right_co($new_s, $old_L, $old_R, cdr($l),
            function ($new_l, $n_L, $n_R) use ($col, $new_s, $old_R)
            {return
                $col(cons($old_R, cons($new_s, $new_l)), $n_L, add1($n_R));
            })
        : (multiinsert_left_right_co($new_s, $old_L, $old_R, cdr($l),
            function ($new_l, $n_L, $n_R) use ($col, $l)
            {return
                $col(cons(car($l), $new_l), $n_L, $n_R);
            }))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            even?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_even
($n)
{return 
    is_eqn($n, x(division($n, 2), 2));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            evens-only*
            </code>
            </td>
            <td>
            {%- highlight php -%}
function evens_only_star
($l)
{return
    is_nulll($l) ? []
    : (is_atom(car($l)) ? 
        is_even(car($l)) ? cons(car($l), evens_only_star(cdr($l)))
        : evens_only_star(cdr($l))
      : cons(evens_only_star(car($l)), evens_only_star(cdr($l))));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            evens-only*&co
            </code>
            </td>
            <td>
            {%- highlight php -%}
function evens_only_star_co
($l, $col)
{return 
    is_nulll($l) ? $col([], 1, 0)
    : (is_atom(car($l)) ?
        is_even(car($l)) ? evens_only_star_co(cdr($l),
            function ($new_l, $product, $sum) use ($col, $l)
            {return 
                $col(cons(car($l), $new_l), x(car($l), $product), $sum);
            })
        : evens_only_star_co(cdr($l),
            function ($new_l, $product, $sum) use ($col, $l)
            {return 
                $col($new_l, $product, plus(car($l), $sum));
            })
      : evens_only_star_co(car($l), 
            function ($a_l, $a_product, $a_sum) use ($col, $l)
            {return
                evens_only_star_co(cdr($l), 
                    function($d_l, $d_product, $d_sum) 
                    use ($col, $l, $a_l, $a_product, $a_sum)
                    {return
                        $col(cons($a_l, $d_l), 
                             x($a_product, $d_product), 
                             plus($a_sum, $d_sum));
                    });
            }));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            the-last-friend
            </code>
            </td>
            <td>
            {%- highlight php -%}
function the_last_friend
($new_l, $product, $sum)
{return
    cons($sum, cons($product, $new_l));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>

<ol>
    <li id="currying"><a href="https://en.wikipedia.org/wiki/Currying" target="_whitephp-ref">Curry-ing</a></li>
    <li id="moses-s"><a href="https://en.wikipedia.org/wiki/Moses_Schönfinkel" target="_whitephp-ref">Moses Schönfinkel</a></li>
    <li id="haskell-c"><a href="https://en.wikipedia.org/wiki/Haskell_Curry" target="_whitephp-ref">Haskell B. Curry</a></li>
    <li id="collector"><a href="https://en.wikipedia.org/wiki/Continuation-passing_style" target="_whitephp-ref">"collector"/"continuation"</a></li>
<p></p>
</ol>
