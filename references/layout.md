# Layout and reveal patterns

Coordinates are in the 1600 × 900 canvas. Most content starts 60–82 px from the left. Panel children use panel-local coordinates. Each slide has a small uppercase eyebrow from its first argument.

- `slide(label, ...parts)` registers a slide. Steps run from 0 for static elements to 1, 2, and onward for reveals. Elements sharing a step appear together. Use consecutive step numbers.
- `title(x,y,size,text,step)` renders a headline. Wrap a word or phrase in braces to highlight it, as in `Next {move}`. Use separate lines when type would run outside the canvas.
- `copy(x,y,text,step,size)` renders supporting text or a short quote.
- `pill(x,y,text,step)` places an independent capsule. Use `pills(x,y,'row',gap,[label,step],...)` or `'stack'` for a group with equal gaps and independent reveals.
- `group(x,y,'stack',gap,...children)` lets the browser measure the preceding element and guarantees a gap below highlighted text. Set children’s x and y to zero in a group.
- `box(x,y,width,height,body,step)` renders a panel. Build the body by concatenating `bar(label)`, `title(...)`, and other element strings. Set child steps at or after the panel's reveal step.
- `grid(x,y,columns,total,filled,cellSize,step,tone,gap)` renders a quantitative grid. Include a readable unit and value. Fractional fills are supported.

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

The first reveal begins after 360 ms and subsequent steps follow at 760 ms intervals. Advance with Right, Space, Page Down, or a click. Previous page starts the sequence again. In full-screen mode, navigation remains available through the keyboard or a click on the slide.
