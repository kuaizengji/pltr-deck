# Layout and reveal patterns

Coordinates are in the 1600 × 900 canvas. Most content starts 60–82 px from the left. Panel children use panel-local coordinates. Each slide has a small uppercase eyebrow from its first argument.

- `slide(label, ...parts)` registers a slide. Steps run from 0 for static elements to 1, 2, and onward for reveals. Elements sharing a step appear together. Use consecutive step numbers.
- `title(x,y,size,text,step)` renders a headline. Wrap a word or phrase in braces to highlight it, as in `Next {move}`. Use separate lines when type would run outside the canvas.
- `copy(x,y,text,step,size)` renders supporting text or a short quote.
- `pill(x,y,text,step)` places an independent capsule. Use `pills(x,y,'row',gap,[label,step],...)` or `'stack'` for a group with equal gaps and independent reveals.
- `group(x,y,'stack',gap,...children)` lets the browser measure the preceding element and guarantees a gap below highlighted text. Set children’s x and y to zero in a group.
- `box(x,y,width,height,body,step)` renders a panel. Build the body by concatenating `bar(label)`, `title(...)`, and other element strings. Set child steps at or after the panel's reveal step.
- `grid(x,y,columns,total,filled,cellSize,step,tone,gap)` renders a quantitative grid. Include a readable unit and value. Fractional fills are supported.

## Information budget

Use one main point per slide. Default to 1–3 supporting points, for a total of 2–4 independent information points. Allow up to 6 in the final visible state for a compact list, a simple process, or a tightly related comparison. Split into additional slides above 6.

Count meaning across the complete slide, including all reveals. Count each distinct assertion, labeled metric, list item, and process stage once. Count a headline if it introduces an assertion. Merge a headline with its restatement or direct numeric expression. Count a value and its unit or time period together. Count a two-part complaint as two claims when each could stand independently. Treat a comparison ratio derived from two displayed values as an additional assertion.

Keep a wrapped sentence as one point. Treat an eyebrow, panel heading, company name used only as a category label, repeated emphasis, source credit, logo, and decorative cells as presentation structure. A label that communicates an independent instruction or benefit still consumes a point.

### Calibration from the 31-slide reference

These counts are editorial judgments based on the reconstructed example's final visible content.

| Reference page | Content | Information points |
| --- | --- | --- |
| 11 | Few salespeople, with a quote restating the surprising sales model | 1 |
| 10 | U.S. commercial becomes dominant, +29% quarter on quarter, +148% year on year, total U.S. revenue +119% year on year | 4 |
| 3 | Political, sociological, anthropological, and financial dimensions, plus AI appearing in the results | 5 |
| 12 | Take the whole market, financial reason, mission reason, customer alpha, sovereignty, warfighter | 6 |
| 16 | Long walk-up, then five stages from talking to hiring salespeople | 6 |

The densest reference layouts reach about 6 under this convention. Use that as the ceiling, with 2–4 as the normal target. A five-stage process may occupy a slide with one framing headline. Give a new argument or a second process its own page. Progressive reveals retain the same total information budget.

Preserve the supplied meaning when splitting. Use a claim slide followed by evidence, a comparison followed by implications, or two consecutive process segments. Keep detailed explanations in speaker notes or supporting material when requested.

## Example

```js
slide('Customer onboarding',
  pills(76,147,'row',12,['Today',1],['Next release',2]),
  group(76,320,'stack',16,
    title(0,0,120,'From signup to {value}',3),
    copy(0,0,'Show users their first result in one session.',4)));

slide('Pilot results',
  title(76,175,105,'{8 of 10} teams activated',1),
  grid(76,350,10,10,8,60,2,orange,8),
  copy(76,470,'One cell represents one pilot team.',2));
```

In automatic mode, the first reveal begins after 360 ms and subsequent steps follow at 760 ms intervals. In manual mode, Right, Space, and clicks reveal one build at a time and advance after the last build. Left reverses a build or returns to the previous page's final state. Page Up and Page Down turn the whole page in either mode. Keep the logo placement area clear if the deck is branded.
