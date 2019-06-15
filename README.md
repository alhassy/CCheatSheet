<h1> Easily Making CheatSheets with Org-mode </h1>

Basics of the tremendously ubiquitous C language that permeates most of computing!

**The listing sheet, as PDF, can be found
 [here](<https://github.com/alhassy/CCheatSheet/blob/master/CheatSheet.pdf>)**,
 while below is an unruly html rendition.

This reference sheet is built around the system
<https://github.com/alhassy/CheatSheet>.


# Table of Contents

1.  [Adminstriva](#orgbda0273)
2.  [Conditionals & Assertion-Based Testing](#org5308c85)
3.  [Assignments](#orgaefd228)
4.  [Loops](#org80fb975)
5.  [Arithmetic and Logic](#org68ae788)
6.  [Strings, Arrays, and Pointers](#org1fd323c)













<a id="orgbda0273"></a>

# Adminstriva

-   All C programs consist of a series of *functions*, which have return values!

-   E.g., Assignment `x = v` is the function that updates the value of name `x`
    with the value of `v` then terminates yielding `v` as a return value.

-   Semicolons act as statement *terminators* &#x2014;in contrast to English,
    wherein they are *separators*.

-   C is whitespace agnostic: Newlines and arbitrary spaces don't matter, for the most part.

-   *Compound statements* are formed from primitive statements by enclosing them in `{` curly braces `}`.
    -   Compounds may appear where-ever a single statement is allowed.

-   All keywords are in lowercase.

-   C comments do *not* nest.
-   Include files personal files by enclosing them in "quotes", use <brackets> for
    standard library files.
-   *All* statements must terminate with a semicolon.
-   Everything must be declared before it can be used &#x2014;sequential.
-   Characters are in-fact aliases for ASCII numerals.

	printf("'A' ≈ %d  ≡  %s", 'A', 'A' == 65? "true" : "false");

	'A' ≈ 65  ≡  true

-   C functions don't have to return anything if it's not appropriate.
    -   E.g., `exit(n)` is the function that returns control to the operating system;
	passing it an argument `n`, usually 0 if everything has gone smoothly and 1 if it's
	an error exit. Yet this function obviously' can't *return* a value.

-   You must specify the type of a variable before you can use it.

-   A variable name is only meaningful in the curly brackets that define it,
    and is otherwise meaningless. This is its *scope*.
    -   Whence, the same names can occur in different places to mean different things.
    -   To transfer data between functions one thus uses parameter lists and return calls.

-   `printf`, “print formatted”, is a *dependently-typed function*: The number and type
    of its arguments depends on its first argument, a string.
    -   The number of occurrences of ‘%’ in the string argument is the number of additional arguments
	the `printf` takes.



<a id="org5308c85"></a>

# Conditionals & Assertion-Based Testing

In C, *true ≈ non-zero*.
Form of the conditional:
\vspace{-0.5em}

    if (condition)
      statementBlock
    // The rest is optional.
    else
      statementBlock

\vspace{-0.5em}

-   `condition` is *any* expression that returns a numeric value:
    All numbers are treated as ‘true’, except 0 which is considered ‘false’.

    <div class="org-center">
    *Asserts are essentially compile-checked comments of user intentions!*
    </div>

`assert(e)` does nothing when expression `e` is true; otherwise it gives a message
showing the filename, function name, line number, and the condition `e` that
failed to be true.

    #include <stdio.h>

    // Disable assertions at compile time by enabling NODEBUG.
    // #define NDEBUG

    #include <assert.h>
    // assert(n)  ≈  if (n) {} else ⟪Terminate and display error message⟫

    int sum(int n)
    {
      int total = 0, i = 0;
      while (i != n + 1)
	total += i, i++;

      return total;
    }

    int main ()
    {
      // print-based testing
      if (1) printf("here"); else printf("there");
      printf("Sum of 0 + 1 + ⋯ + 99 + 100 = %d", sum(100));

      // assertion-based testing
      assert( sum(100) == 5050 );
      assert( (1 ? "here" : "there") == "here" );

      // Is completely ignored if the #define is enabled.
      // assert(0);  // Otherwise, this causes a crash.

      return 0;
    }

    hereSum of 0 + 1 + ⋯ + 99 + 100 = 5050

  \vspace{-0.5em}
Enforce a particular precedence order by enclosing expressions in parentheses.

    == equals          != differs from     !  not
    >= at least        <= at most          && and
    >  greater than    <  less than        || or



<a id="orgaefd228"></a>

# Assignments

    /* Abbreviations */
      x ⊕= y   ≈  x = x ⊕ y
      x++       ≈  x += 1
      --x      ≈  x -= 1

The increment and decrement, `++/--`, operators may precede or follow a name:

-   If they follow a name, then their behaviour is executed *after* the smallest context
    &#x2014;e.g., braces or conditional parentheses&#x2014; in which they occur.

-   When they precede a name, their behaviour is executed before the context in which
    they appear.

-   The order of evaluation is not specified inside a function call and so behaviour
    varies between compilers.

**Avoid using these in complex expressions, unless you know what you're doing.**


<a id="org80fb975"></a>

# Loops

Here's the general form.

    while (condition)
      statementBlock

    /* Abbreviations */
    /* for      loop */   for(A; B; C;) S  ≈  A; while(B) S
    /* do-while loop */   do S while B     ≈  S; while(B) S

do/while: The conditional is evaluated *after* the statement has been executed
and so the statement is obeyed at least once, regardless of the truth or falsity of
the condition. This is useful for *do once, and possible more* operations.

    int i = 0;
    do printf("%d \n", i++);
    while (i != 10); //Note the ending semicolon.

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />
</colgroup>
<tbody>
<tr>
<td class="org-right">0</td>
</tr>


<tr>
<td class="org-right">1</td>
</tr>


<tr>
<td class="org-right">2</td>
</tr>


<tr>
<td class="org-right">3</td>
</tr>


<tr>
<td class="org-right">4</td>
</tr>


<tr>
<td class="org-right">5</td>
</tr>


<tr>
<td class="org-right">6</td>
</tr>


<tr>
<td class="org-right">7</td>
</tr>


<tr>
<td class="org-right">8</td>
</tr>


<tr>
<td class="org-right">9</td>
</tr>
</tbody>
</table>



<a id="org68ae788"></a>

# Arithmetic and Logic

> *&#x2026;and then the different branches of arithmetic &#x2014;Ambition, Distraction,
> Uglification, and Derision.*
>
> &#x2014;Alice's Adventures in Wonderland

The modulus operator `%` gives the *remainder* of a division.

    printf("rem = 10 %% 3 = %d  ⇒  ∃ quot •  10 = 3 × quot + rem  ∧  quot = %d", 10 % 3, 10 / 3);

    rem = 10 % 3 = 1  ⇒  ∃ quot •  10 = 3 × quot + rem  ∧  quot = 3

-   In conditionals, one may see `n % d` to mean that `n % d` is true, i.e., is *non-zero*.
    This expresses that `n` is a *multiple* of `d`.

-   That is, numerically `%` yields remainders; but logically, in C, it expresses the
    is-multiple-of relationship.

When `x` is a number, the shift operations correspond to multiplication and
division by `2ⁿ`, respectively.

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-left">Left Shift</td>
<td class="org-left">`x << n`</td>
<td class="org-left">append the bit representation of `x` with `n`-many 0s</td>
</tr>


<tr>
<td class="org-left">Right Shift</td>
<td class="org-left">`x >> n`</td>
<td class="org-left">throw away `n` bits from the end of the bit representation of `x`</td>
</tr>
</tbody>
</table>

The *bitwise* operators *and `&`, or `|`, not `!`,* and *xor* `^` operate at the bit representation
of an item. For example, the ASCII code of a character consists of 7 bits where

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-right"><span class="underline">Bit</span></td>
<td class="org-left"><span class="underline">Function</span></td>
</tr>


<tr>
<td class="org-right">7</td>
<td class="org-left">0 digit, 1 letter</td>
</tr>


<tr>
<td class="org-right">6</td>
<td class="org-left">0 upper case, 1 digit or lower case</td>
</tr>


<tr>
<td class="org-right">5</td>
<td class="org-left">0 for a-o, 1 for digit or p-z</td>
</tr>
</tbody>
</table>

Whence, to convert a character to uppercase it suffices to change bit 5 to be a 0
and leave the other bits alone. That is, to perform a bitwise *and* with the binary
number *11011111*, which corresponds to the decimal number 223.

    // Mask, or hide, bit  6 to be a ‘1’.
    #define toLower(c) (c | (1 << 6))

    #define toUpper(c) (c & 223)

    #define times10(x) ( (x << 1)  +  (x << 3)) // Parens matter!
    // x  ⇒  2·x + 8·x  ⇒  10 · x

How did we know is was 223?

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<tbody>
<tr>
<td class="org-left">0. Ninth bit is on</td>
<td class="org-left">`100000000`</td>
<td class="org-left">`1 << 8`</td>
</tr>


<tr>
<td class="org-left">1. Negate it: Eight ones</td>
<td class="org-left">`11111111`</td>
<td class="org-left">`(1 << 8)`</td>
</tr>


<tr>
<td class="org-left">2. Sixth bit is on</td>
<td class="org-left">`100000`</td>
<td class="org-left">`1 << 5`</td>
</tr>


<tr>
<td class="org-left">3. Xor them</td>
<td class="org-left">`11011111`</td>
<td class="org-left">`⋯ ^ ⋯`</td>
</tr>


<tr>
<td class="org-left">4. See it as a decimal</td>
<td class="org-left">`223`</td>
<td class="org-left">&#xa0;</td>
</tr>
</tbody>
</table>

Ironically, C has no primitive binary printing utility.



<a id="org1fd323c"></a>

# Strings, Arrays, and Pointers

-   The idea of a pointer is central to the C programming philosophy.
    -   It is pointers to strings, rather than strings themselves, that're passed around
	in a C program.

-   C strings like `s = "this"` actually, under the hood, are *null-terminated
    arrays of characters*: The name `s` refers to the *address of* the first character, the `'t'`,
    with the array being `'t' → 'h' → 'i' → 's' → 𝟘`, where 𝟘 is *not* ASCII zero
    &#x2014;whose value is 48&#x2014; but ASCII *null* &#x2014;i.e., all bits set to 0.

-   *An array name is a pointer to the beginning of the array.*
    -   Yet, an array name is a constant and you can't do arithmetic with it.

    int length(char c[]) // A string is a character array
    {
      // While c[l] is not an ASCII null, keep counting until.
      int l = 0;
      while( c[l] ) l++;
      return l;
    }

    int main()
    {
      char str[] = "hello world 0123";
      printf("length(“%s”) = %d", str, length(str));
       return 0;
    }

    length(“hello world 0123”) = 16

-   `T *p;` ⇒ declare `p` to be a pointer to elements of type `T`.
-   `*p = v` ⇒ “put the value of `v` in the location which `p` points to”

We can now rewrite the length function with even less square brackets.

    int length(char* c)
    {
      char* start = c;
      while( *c ) c++; // Local copy of c is affected.
      return c - start;
    }

    assert(length("hello world") == 11);
