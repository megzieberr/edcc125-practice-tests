# EDCC125 practice tests

Five open-book, 50-question practice tests for the EDCC125 exam (History of Education, textbook units 1 to 4).
One self-contained `index.html`, no build step, no server, no tracking. Scores and half-finished tests are kept in
the browser's own storage on the device that took the test, nowhere else.

Live: https://megzieberr.github.io/edcc125-practice-tests/

## How it behaves
- Test picker for Tests 1 to 5. A test with `ready:false` shows "Coming soon".
- Question order is fixed. Options shuffle every time a test starts, except true/false questions (`tf:true`).
- Progress saves as you go, so a refresh or closed tab can be resumed.
- "Mark my test" warns about blanks, then marks. The review shows every question with the right answer, the pick,
  why, and the textbook source. "Show only my mistakes" filters the review.
- Best and last score per test show on the picker.

## Adding a test (for the person building Tests 2 to 5)
The question plan is in the study folder: `EDDC125\Semester Test (Exam)\TEST-PLAN.md`. Build exactly the rows of
your test, in order.

In `index.html`, find the `TESTS` array near the top of the script. Tests 2 to 5 already have placeholder objects:

```js
{ id:"t2", num:2, title:"Test 2", ready:false, desc:"Coming soon.", qs:[] },
```

Replace your placeholder with the full test, keeping the same `id`, `num` and `title`, and set `ready:true`:

```js
{ id:"t2", num:2, title:"Test 2", ready:true,
  desc:"Mixed units 1 to 4. Includes the real Africa-reasons exam question.",
  qs:[
    { ref:"U3-01",
      q:"The reasons for studying the history of education in Africa include the following. Which statement is incorrect?",
      o:["...","...","...","...","If all of these are correct, mark here"],
      c:3,
      why:"One or two plain sentences: why this is right, and the trap.",
      src:"Textbook §3.1" },
    { ref:"U2-06", q:"The earliest excavated classroom, from about 2000 BC, was found in a temple.",
      o:["True","False"], c:1, tf:true,
      why:"False. It was found in a palace.", src:"Textbook Ch 2: the first schools" },
    { ref:"X-01", q:"Which of these happened in 1960?",
      list:["Africa's adult literacy rate was about 9%","The Sharpeville massacre","The Addis Ababa meeting","The whites-only republic referendum"],
      o:["A and B","A, B and D","C and D","All of these","None of these"], c:1,
      why:"...", src:"Textbook §3.6, §3.8, §4.9" }
    // ... 50 questions in total
  ]},
```

### Question fields
| Field | Required | Meaning |
|---|---|---|
| `ref` | yes | The plan's item key (e.g. `U3-01`, `E2-Q11`, `ART-u1b-Q9`, `FIX-E3-Q21`, `P-X1`). Not shown on the page; it is for checking. |
| `q` | yes | The question stem, plain text. |
| `o` | yes | 2 to 5 options, plain text. Put the mark-here option wherever the source has it; it shuffles with the rest. |
| `c` | yes | Index (0-based) of the correct option in `o`, before shuffling. |
| `tf` | for true/false | `true` keeps the options in the given order (`["True","False"]`, or the joke `["True","Usually","False"]`). |
| `list` | combos only | Statements shown under the stem as A), B), C)...; the combo options refer to these letters. |
| `why` | yes | Short reason for the answer, shown after marking. |
| `src` | yes | Where it is: "Textbook §4.10", "Textbook Ch 2, p. 30", "QC 2 slide 42". |

### Rules
- English only. Max 5 options. Plain text only (no HTML in the strings). Use curly quotes “ ” inside strings to
  avoid escaping.
- No em-dashes. No names of students or the lecturer anywhere (historical figures and cited authors are fine).
- After editing: open the page at phone width (375 px), take the test once, check the marking, re-check every key
  against the plan's source, then commit and push to `main`. GitHub Pages redeploys in about a minute.
