This project is based off Low Level JavaScripts video (https://www.youtube.com/watch?v=sRWE5tnaxlI) where he shows a way to make executable JavaScript only using the following characters ({[/>+!-=\]}).

This version of the code is focused on optimizing the output a little more in order to get a shorter string in total.
With the old one `compile('console.log("Hello world!");')` would return a string with length of 117,711 characters
but with the new one, we only get a length of 99,292.

This as you could imagine is a big difference being ~18k characters (So about 18KB less).

## So how did I do this?
My first thought when watching him explain it is "There has to be a better way of doing numbers 10+ instead of adding 1 constantly",
and so I got to playing around with it a little and found that since 1 + [] + 2 = 12 (because [] + x changes the coercion type to a string) I figured that all you need is the numbers 0 - 9 and you can make any number with them.

This in fact did work though I ran into some issues with it being a string type at the end any of the ones that converted the charCode into the string were getting confused as it was already a string (Eg, ``map.d = `(${number(13)})[${fromString('toString')}](${number(14)})`;`` this just returned 13.)

My fix for this method was very simple I just add a + in front of the number string (so from `(+!![]) + [] + (+!![] +!![])` to `+((+!![]) + [] + (+!![] +!![]))` and there we go, all done made more efficient
