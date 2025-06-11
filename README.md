# ocaml-project-3-regular-expression-engine-solved
**TO GET THIS SOLUTION VISIT:** [OCAML-Project 3 Regular Expression Engine Solved](https://mantutor.com/product/ocaml-project-3-regular-expression-engine-solved/)


---

**For Custom/Order Solutions:** **Email:** mantutorcodes@gmail.com  

*We deliver quick, professional, and affordable assignment help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;66309&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;OCAML-Project 3 Regular Expression Engine Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
In this project you will implement algorithms to work with NFAs, DFAs, and regular expressions. In particular, you will implement an `accept` function to see whether a string is matched by a NFA; you will write a `nfa_to_dfa` function to convert an NFA to a DFA using the subset construction; and you will write a `regex_to_nfa` function to convert a regular expression to an NFA. You will also implement several other helper functions to assist in these tasks.

The project is broken into three parts: algorithms on NFAs; converting a DFA to an NFA; and converting/working with Regular Expressions. NFAs and DFAs are implemented in `src/nfa.ml`, and regexes in `src/regex.ml`.

In class we implemented a Regular Expression Interpreter through a series of reductions. First convert the RegExp to an NFA, then the NFA to a DFA, and then run the DFA on an input string to see if the string is accepted. This project will not follow that sequence exactly, but will allow you to work with the reductions so you understand each step in the sequence.

Here’s how the parts can be assembled into an Interpreter. In Part I you’ll simulate an NFA. You can do that directly, or you can use Part II to convert to a DFA and then assume you have a DFA to simulate. In Part II you’ll implement an NFA to DFA converter. In Part III you’ll convert a RegExp to an NFA. You can put these parts together to create an Interpreter: Input a RegExp to Part III to create an NFA, and then input that NFA and a string to Part I to simulate the resulting NFA. Or, input that NFA to Part II to get a DFA, then since the class of DFAs is a subset of NFAs, input that DFA to Part I to simulate it. You aren’t required to create these workflows, as we’ll test each part independently, but you can experiment with them. (Note that the same Ocaml type, `nfa_t`, is used for both NFAs and DFAs in this project, so the function to convert an NFA to a DFA takes an `nfa_t` to an `nfa_t`.)

## Part 1: NFAs

This first part of the project asks you to implement some functions for working with NFAs. In particular, you will be asked to implement the *move* and *epsilon closure* functions [described in class][lecture notes]; these will be handy for Part 2. You will also implement an `accept` function to determine whether a string is matched by a given NFA; both *move* and *epsilon closure* may be handy here, too.

### NFA Types

Before starting, you’ll want to familiarize yourself with the types you will be working with.

The type `nfa_t` is the type representing NFAs. It is modeled after the formal definition of an NFA, a 5-tuple (Σ, Q, q0, F, δ) where:

1. Σ is a finite alphabet,

2. Q is a finite set of states,

3. q0 ∈ Q is the start state,

5. F ⊆ Q is the set of accept states, and

4. δ : Q × (Σ ∪ {ε}) → 𝒫(Q) is the transition function (𝒫(Q) represents the powerset of Q).

We translate this definition into OCaml in a straightforward way using record syntax:

“`ocaml

type (‘q, ‘s) transition = ‘q * ‘s option * ‘q

type (‘q, ‘s) nfa_t = {

sigma : ‘s list;

qs : ‘q list;

q0 : ‘q;

fs : ‘q list;

delta : (‘q, ‘s) transition list;

}

“`

Notice the types are parametric in state `’q` and symbol `’s`.

The type `transition` represents NFA transitions. For example:

“`ocaml

let t1 = (0, Some ‘c’, 1)&nbsp; (* Transition from state 0 to state 1 on character ‘c’ *)

let t2 = (1, None, 0)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (* Transition from state 1 to state 0 on epsilon *)

“`

While the formal definition of a transition is a function which maps a state and character to a set of states, we will define transitions as 3-tuples so that each edge in the NFA will correspond to a single transition in the list of transitions. This will make the syntax for defining NFAs cleaner, and allows for a one-to-one mapping between elements of the transition list and edges in the NFA graph.

An example NFA would be:

“`ocaml

let nfa_ex = {

sigma = [‘a’];

qs = [0; 1; 2];

q0 = 0;

fs = [2];

delta = [(0, Some ‘a’, 1); (1, None, 2)]

}

“`

This looks like:

![NFA m](images/m_viz.png)

Here is a DFA:

“`ocaml

let dfa_ex = {

sigma = [‘a’; ‘b’; ‘c’];

qs = [0; 1; 2];

q0 = 0;

fs = [2];

delta = [(0, Some ‘a’, 1); (1, Some ‘b’, 0); (1, Some ‘c’, 2)]

}

“`

This looks like:

![NFA n](images/n_viz.png)

### Functions

Here are the functions you must implement:

#### `move nfa qs s`

– **Type**: `(‘q, ‘s) nfa_t -&gt; ‘q list -&gt; ‘s option -&gt; ‘q list`

– **Description**: This function takes as input an NFA, a list of initial states, and a symbol option. The output will be a list of states (in any order, with no duplicates) that the NFA might be in after making one transition on the symbol (or epsilon if None), starting from one of the initial states given as an argument to move. If `c` is not in the alphabet (`sigma`), then return the empty list.

– **Examples**:

“`ocaml

move nfa_ex [0] (Some ‘a’) = [1] (* nfa_ex is the NFA defined above *)

move nfa_ex [1] (Some ‘a’) = []

move nfa_ex [2] (Some ‘a’) = []

move nfa_ex [0;1] (Some ‘a’)&nbsp; = [1]

move nfa_ex [1] None = [2]

“`

– **Explanation**:

1. Move on `nfa_ex` from `0` with `Some a` returns `[1]` since from 0 to 1 there is a transition with character `a`.

2. Move on `nfa_ex` from `1` with `Some a` returns `[]` since from 1 there is no transition with character `a`.

3. Move on `nfa_ex` from `2` with `Some a` returns `[]` since from 2 there is no transition with character `a`.

4. Move on `nfa_ex` from `0` and `1` with `Some a` returns `[1]` since from 0 to 1 there is a transition with character `a` but from 1 there was no transition with character `a`.

5. Notice that the NFA uses an implicit dead state. If `s` is a state in the input list and there are no transitions from `s` on the input character, then all that happens is that no states are added to the output list for `s`.

6. Move on `nfa_ex` from `1` with `None` returns `[2]` since from 1 to 2 there is an epsilon transition.

#### `e_closure nfa qs`

– **Type**: `(‘q, ‘s) nfa_t -&gt; ‘q list -&gt; ‘q list`

– **Description**: This function takes as input an NFA and a list of states. The output will be a list of states (in any order, with no duplicates) that the NFA might be in making zero or more epsilon transitions, starting from the list of initial states given as an argument to `e_closure`. You can assume you will always be passed in a state that is in `nfa`’s states list.

– **Examples**:

“`ocaml

e_closure nfa_ex [0] = [0]

e_closure nfa_ex [1] = [1;2]

e_closure nfa_ex [2]&nbsp; = [2]

e_closure nfa_ex [0;1] = [0;1;2]

“`

– **Explanation**:

1. e_closure on `nfa_ex` from `0` returns `[0]` since there is no where to go from `0` on an epsilon transition.

2. e_closure on `nfa_ex` from `1` returns `[1;2]` since from `1` you can get to `2` on an epsilon transition.

3. e_closure on `nfa_ex` from `2` returns `[2]` since there is no where to go from `2` on an epsilon transition.

4. e_closure on `nfa_ex` from `0` and `1` returns `[0;1;2]` since from `0` you can only get to yourself and from `1` you can get to `2` on an epsilon transition but from `2` you can’t go anywhere.

#### `accept nfa s`

– **Type**: `(‘q, char) nfa_t -&gt; string -&gt; bool`

– **Description**: This function takes an NFA and a string, and returns true if the NFA accepts the string, and false otherwise. You will find the functions in the [`String` module][string doc] to be helpful. (You might find it useful to use `nfa_to_dfa`, implemented in Part 2 below, as part of your `accept` implementation, but this is not required.)

– **Examples**:

“`ocaml

accept dfa_ex “” = false&nbsp; (* dfa_ex is the NFA defined above *)

accept dfa_ex “ac” = true

accept dfa_ex “abc” = false

accept dfa_ex “abac” = true

“`

– **Explanation**:

1. accept on `dfa_ex` with the string “” returns `false` because initially we are at our start state 0 and there are no characters to exhaust and we are not in a final state.

2. accept on `dfa_ex` with the string “ac” returns `true` because from 0 to 1 there is an ‘a’ transition and from 1 to 2 there is a ‘c’ transition and now that the string is empty and we are in a final state thus the nfa accepts “ac”.

3. accept on `dfa_ex` with the string “abc” returns `false` because from 0 to 1 there is an ‘a’ transition but then to use the ‘b’ we go back from 1 to 0 and we are stuck because we need a ‘c’ transition yet there is only an ‘a’ transition. Since we are not in a final state thus the function returns false.

4. accept on `dfa_ex` with the string “abac” returns `true` because from 0 to 1 there is an ‘a’ transition but then to use the ‘b’ we go back from 1 to 0 and then we take an ‘a’ transition to go to state 1 again and then finally from 1 to 2 we exhaust our last character ‘c’ to make it to our final state. Since we are in a final state thus the nfa accepts “abac”.

## Part 2: DFAs

In this part, our goal is to implement the `nfa_to_dfa` function. It uses the subset construction to convert an NFA to a DFA. For help with understanding Subset Construction you can look at the [lecture notes][lecture notes] and [here][subset construct]. We recommend you implement the `move` and `e_closure` parts of Part 1 before starting Part 2, since they are used in the subset construction.

Remember that every DFA is also an NFA, but not the other way around. Recall that the subset construction converts an NFA to a DFA by grouping together multiple NFA states into a single DFA state. Hence, our DFA type is `(‘q list, ‘s) nfa_t`. Notice that our

states are now lists (representing sets) of states from the NFA.

To write `nfa_to_dfa` we will &nbsp;write some helpers. These helpers follow the NFA to DFA conversion method discussed in lecture. We will test these functions individually in the public tests to help you track your progress and find bugs. Remember, you can always add more student tests in `test/student.ml`! **Hint**: `new_states`, `new_trans`, and `new_finals` can all be implemented in one line!

#### `new_states nfa qs`

– **Type**: `(‘q, ‘s) nfa_t -&gt; ‘q list -&gt; ‘q list list`

– **Description**: Given an NFA and a list of states from that NFA (a single state in the DFA) computes all the DFA states that you can get to from a transition out of `qs` (including the dead state). You can return the list in any order, with or without duplicates. Dead states are represented by empty lists. *Note: each element in the list corresponds to all of the states you can get to from one character of the alphabet (`sigma`) followed by any number of epsilon transitions*

– **Examples**:

“`ocaml

new_states nfa_ex [0] = [[1; 2]]

new_states dfa_ex [0; 1] = [[1]; [0]; [2]]

“`

#### `new_trans nfa qs`

– **Type**: `(‘q, ‘s) nfa_t -&gt; ‘q list -&gt; (‘q list, ‘s) transition list`

– **Description**: Given an NFA and a list of states from that NFA (a single state in the DFA) computes all the transitions coming from `qs` (including the dead state) in the DFA.

– **Examples**:

“`ocaml

new_trans dfa_ex [0; 1] = [([0; 1], Some ‘a’, [1]); ([0; 1], Some ‘b’, [0]); ([0; 1], Some ‘c’, [2])]

“`

#### `new_finals nfa qs`

– **Type**: `(‘q, ‘s) nfa_t -&gt; ‘q list -&gt; ‘q list list`

– **Description**: Given an NFA and a list of states from that NFA (a single state in the DFA) returns `[qs]` if `qs` is final in the DFA and `[]` otherwise.

– **Examples**:

“`ocaml

new_finals dfa_ex [0; 1; 2] = [[0; 1; 2]]

new_finals dfa_ex [0; 1] = []

“`

#### `nfa_to_dfa nfa`

– **Type**: `(‘q, ‘s) nfa_t -&gt; (‘q list, ‘s) nfa_t`

– **Description**: This function takes as input an NFA and converts it to an equivalent DFA. The language recognized by an NFA is invariant under `nfa_to_dfa`. In other words, for all NFAs `nfa` and for all strings `s`, `accept nfa s = accept (nfa_to_dfa nfa) s`.

### Suggestion

The `nfa_to_dfa` algorithm is pretty substantial. While you are free to design it in whatever manner you like (referring the [lecture slides][lecture notes] and [notes][subset construct] for assistance), we suggest you consider writing a helper function **nfa_to_dfa_step** that does most of the work. This function is invoked for each iteration of the algorithm. Here is its description:

#### `nfa_to_dfa_step nfa dfa wrk`

– **Type**: `(‘q, ‘s) nfa_t -&gt; (‘q list, ‘s) nfa_t -&gt; ‘q list list -&gt; (‘q list, ‘s) nfa_t`

– **Description**: First, let’s take a look at what is being passed into the function for clarity:

*Parameters*

* `nfa`: the NFA to be converted into a DFA.

* `dfa`: the DFA to be created from the NFA. This will act as the accumulator in the function. Each time this function is called, the DFA should be updated based on the worklist.

* `wrk`: a list of unvisited states.

Given an NFA, a partial DFA, and a worklist, this function will compute one step of the subset construction algorithm. This means that we take an unvisited DFA state from the worklist and add it to our DFA that we are creating (updating the list of all states, transitions, and final states appropriately). Our worklist is then updated for the next iteration by removing the newly processed state. You will want to use the previous three functions as helpers. They can be used to update the DFAs states, transistions, and final states.

Once again, you are free to skip implementing this function if you feel you have a better approach.

## Part 3: Regular Expressions

For the last part of the project, you will implement code to convert a regular expression (in the format given below) to an NFA. (Then you could use your `NFA` module developed above to match particular strings.) The `Regexp` module represents a regular expression with the type `regexp_t`:

“`ocaml

type regexp_t =

| Empty_String

| Char of char

| Union of regexp * regexp

| Concat of regexp * regexp

| Star of regexp

“`

This datatype represents regular expressions as follows:

* `Empty_String` represents the regular expression recognizing the empty string (not the empty set!). Written as a formal regular expression, this would be `epsilon`.

* `Char c` represents the regular expression that accepts the single character c. Written as a formal regular expression, this would be `c`.

* `Union (r1, r2)` represents the regular expression that is the union of r1 and r2. For example, `Union(Char ‘a’, Char’b’)` is the same as the formal regular expression `a|b`.

* `Concat (r1, r2)` represents the concatenation of r1 followed by r2. For example, `Concat(Char ‘a’, Char ‘b’)` is the same as the formal regular expresion `ab`.

* `Star r` represents the Kleene closure of regular expression r. For example, `Star (Union (Char ‘a’, Char ‘b’))` is the same as the formal regular expression `(a|b)*`.

Here is the function you must implement:

#### `regexp_to_nfa regexp`

– **Type**: `regexp_t -&gt; nfa_t`

– **Description**: This function takes a regexp and returns an NFA that accepts the same language as the regular expression. Notice that as long as your NFA accepts the correct language, the structure of the NFA does not matter since the NFA produced will only be tested to see which strings it accepts. Remember, `Empty_String` represents the regular expression recognizing `epsilon`, as stated above.

## Provided Functions

The rest of these functions are implemented for you as helpers. Use them as you like; you don’t have to modify them.

#### `explode s`

– **Type**: `string -&gt; char list`

– **Description**: This function takes a string and converts it into a character list. The following function may be helpful when writing `accept` in Part 1.

#### `fresh`

– **Type**: `unit -&gt; int`

– **Description**: This function takes in type `unit` as an argument (similar to Null). This function uses imperative OCaml to return an `int` value that has not been used before by using a reference to a counter. You might find this helpful for implementing&nbsp; `regexp_to_nfa`.

– **Examples**:

“`ocaml

fresh() = 1

fresh() = 2

fresh() = 3

…

“`

The next two functions rely on your code for correctness!

#### `string_to_nfa s`

– **Type**: `string -&gt; nfa`

– **Description**: This function takes a string for a regular expression, parses the string, converts it into a regexp, and transforms it to an nfa, using your `regexp_to_nfa` function. As such, for this function to work, your `regexp_to_nfa` function must be working. In the starter files we have provided function `string_to_regexp` that parses strings into `regexp` values, described next.

#### `string_to_regexp s** (provided for yo`

– **Type**: `string -&gt; regexp`

– **Description**: This function takes a string for a regular expression, parses the string, and outputs its equivalent regexp. If the parser determines that the regular expression has illegal syntax, it will raise an IllegalExpression exception.

– **Examples**:

“`ocaml

string_to_regexp “a” = Char ‘a’

string_to_regexp “(a|b)” = Union (Char ‘a’, Char ‘b’)

string_to_regexp “ab” = Concat(Char ‘a’,Char ‘b’)

string_to_regexp “aab” = Concat(Char ‘a’,Concat(Char ‘a’,Char ‘b’))

string_to_regexp “(a|E)*” = Star(Union(Char ‘a’,Empty_String))

string_to_regexp “(a|E)*(a|b)” = Concat(Star(Union(Char ‘a’,Empty_String)),Union(Char ‘a’,Char ‘b’))

“`

In a call to `string_to_regexp s` the string `s` may contain only parentheses, |, \*, a-z (lowercase), and E (for epsilon). A grammatically ill-formed string will result in `IllegalExpression` being thrown. Note that the precedence for regular expression operators is as follows, from highest(1) to lowest(4):

Precedence | Operator | Description

———- | ——– | ———–

1 | `()` | parentheses

2 | `*` | closure

3 | &amp;nbsp; | concatenation

4 | &lt;code&gt;&amp;#124;&lt;/code&gt; | union

Also, note that all the binary operators are **right associative**.
