# qlocka2

A software version of the [Qlocktwo](https://qlocktwo.com/en/), in Swedish and with minimal code.

## Layout

The original Swedish Qlocktwo layout is 11x10 characters.

```
KLOCKAN ÄR
FEMKVARTIO
TJUGO ÖVER
I HALV ETT
TVÅTREFYRA
FEMSEX SJU
ÅTTANIOTIO
ELVA  TOLV
```

This letter layout is only 10x8 characters. One neat hack is to combine three of the minute words into one on line 2: 

`FEMKVARTIO` accomodates either `FEM`, `KVART` or `TIO` (which are never displayed at the same time for minute words).


## Minimal code

My original ambition was to reach less than 1K for HTML, CSS and JS. I haven't reached that, but I'm pretty close.

- The HTML has been minimized through omitting some HTML tags that are not required by the HTML5 standard; `<html>`, `<head>`, `<body>`...
- The JS has been minimized through a series of dirty hacks. I haven't tested it out thouroughly yet so no guarantees that it is always correct.
  - It's smaller to have a string with comma separated values and `split(',')` it than to declare an array of strings
  - It's smaller to declare an array with empty holes `["",,,,,"FEM ÖVER"]` than to allocate specific positions `arr[5] = "FEM ÖVER"`
  - It's *sometimes* smaller to reuse the numerals from the numeral array, depending on the length of the word
  
## Cheating

For a larger codebase I would improve the timers. 

- The initial render starts only after 1s, I'd render once immediately
- The update doesn't actually happen exactly on the new second, which is imprecise. I'd set an initial timeout for the next tick (ever 5 minutes for this type of clock) and then run a setInterval for each 5 minutes.
- Browser compatibility: I'm relying on string templates, Array.map so older browsers not compatible.
- Unit testing: I didn't create any unit tests! I'm sure they would be useful since I discovered many mistakes as I kept developing.

